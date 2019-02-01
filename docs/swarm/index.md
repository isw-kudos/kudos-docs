# Docker Swarm

## General

- Logging is not so reliable, look into custom logging drivers. logstash?
- Delivery model? script?
- Role to deploy Mongo
- Role to deploy Boards and Ideas
- Role to deploy with buzzy image
- Resource allocation through compose
- Resource monitoring? Does portainer do that?

## SECURITY

- Storage is on externally accessible machine?!
  - but nfs server is only allowed on local ip mask
- mongodb auth + add creds
- docker repo access config is basic auth

## STEPS - OUTLINE:

### Gateway + storage

1. Create a CentOS 7 host with external IP
2. Map DNS to instance
3. Set up NFS Server
4. Install docker + docker-compose
5. Deploy nginx load balancer via docker-compose

### Create swarm

1. Create CoreOS hosts
2. Connect all nodes into a swarm
3. Set up proxy and portainer
4. Set up docker config to access private image repo
5. Deploy app with required config and images

## STEPS - MANUAL:

### Setup NFS server in centos

```
sudo su
firewall-cmd --permanent --zone=public --add-service=nfs
firewall-cmd --reload
yum -y install nfs-utils
systemctl enable nfs-server.service
systemctl start nfs-server.service
mkdir -p /data/nfs
chown -R nfsnobody:nfsnobody /data
chmod -R 755 /data
echo "/data/nfs 10.142.0.1/24(rw,sync,no_subtree_check,no_root_squash)" >> /etc/exports
exportfs -a
```

### Install Docker & Docker-compose on CentOS

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker support
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### RUN NGINX LOAD BALANCER

- From local machine transfer docker compose and other config :
  `gcloud compute scp . support@gateway-1:/opt/setup/ --recurse`
- On gateway node:

```
cd /opt/setup
 docker-compose up -d 
```

### Create Node Swarm

```
docker swarm init
docker swarm join-token manager
<run printed join command>
```

### Mount NFS ON all swarm nodes

```
sudo mkdir -p /data/nfs && sudo mount 10.142.0.5:/data/nfs /data/nfs
```

### Deploy proxy & portainer

- On a swarm manager node-1:

```
sudo mkdir /opt/setup -p
sudo chmod -R +777 /opt
```

- From local machine transfer remote files:

```
gcloud compute scp . support@node-1:/opt/setup/ --recurse
```

- On a swarm manager node-1:

```
cd /opt/setup
# configure repo credentials
mkdir -p ~/.docker && cp config.json ~/.docker/config.json

# create network for proxy
docker network create --driver=overlay --internal=false proxy

# create required dirs and move ssl
sudo mkdir /data/nfs/sslcerts
sudo mkdir /data/nfs/portainer
sudo mv /opt/setup/ssl/* /data/nfs/sslcerts

# deploy proxy & portainer
docker stack deploy -c proxy.yml proxy
docker stack deploy -c portainer.yml portainer
```

### Optional commands/steps

- deploy app with registry auth
  `docker stack deploy -c app.yml app --with-registry-auth`

- commands to exec based on service_name

```
docker exec -ti service_name.1.$(docker service ps -f 'name=service_name.1' service_name -q --no-trunc | head -n1) sh
```

- Mongo replica set

```
docker exec -ti m_mongo1.1.$(docker service ps -f 'name=m_mongo1.1' m_mongo1 -q --no-trunc | head -n1) bash
mongo
> rs.initiate( {
   _id : "rs0",
   members: [
      { _id: 0, host: "mongo1:27017" },
      { _id: 1, host: "mongo2:27017" },
      { _id: 2, host: "mongo3:27017" }
   ]
})
#test connection
mongo --host rs0/mongo1:27017,mongo2:27017,mongo3:27017
mongo "mongodb://mongo1:27017,mongo2:27017,mongo3:27017/myDB?replicaSet=rs0"
```

- Sticky sessions - add following label to container
  `traefik.backend.loadbalancer.stickiness=true`

- Docker-compose in CoreOS for debugging stack ymls

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /opt/bin/docker-compose
sudo chmod +x /opt/bin/docker-compose
```

## Gotchas

- Volumes need to be manually removed on all nodes if they are broken or config is updated, they are not removed as part of the stack
- traefik labels need to be on the container not on the service, i.e. under `deploy:`
