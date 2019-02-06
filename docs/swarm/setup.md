## Overview / Introduction

While there are many ways to setup a docker swarm environment, this document will step through setting up a reasonable environment that includes:

- Shared storage with nfs
- http(s) proxy _traefik_
- Database _mongo_
- File storage _minio_
- Management interface _portainer_
- Logging _elk stack_ - (optional)
- Monitoring _prometheus/grafana_ - (optional)

---

## Server information

As the name swarm suggests, this setup is designed to run across a number of servers (referred to as nodes). ISW recommends that the minimum number of servers you should start with is 4, being one for the NFS server and http gateway and 3 swarm managers. You may start with small VMs to set this up and expand them as your need increases (either by extending cores and ram on the existing servers or by adding more manager/worker nodes to your swarm).

This document will assume the following setup:

- Gateway server (CentOS)
- 3 Swarm managers (CoreOS)

If you have more managers or workers just extend the config where indicated below.

If you are testing this setup, you can get away with quite small servers (we have had success with 2 cores and 1.7gb ram) however if you plan to include the logging and/or monitoring services then you should expect to dedicate an additional 2gb ram minimum for each of these sevices.

---

## Network setup

The setup below will establish some internal networking rules to help protect your environment.  
When configuring the servers, you will need to enable the following network rules:

- http(s) traffic should be allowed to the Gateway only
- ssh traffic should be allowed to all servers
- Where possible all servers should be on an additional (internal only) subnet, this allows us to further lock down access to NFS shares

---

## Setup Ansible

Throughout this guide we will use ansible to setup the servers and deploy services (stacks) to the swarm.

If you have access to a Mac or Linux machine, [follow these instructions](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) to get up and running.

Whilst that document states windows is not supported, ISW has had much success running ansible under windows by enabling WSL (Windows subsystem for Linux), installing Ubuntu for the windows store and proceeding with the Ubuntu instructions linked.

Refer to [this document from Microsoft](https://docs.microsoft.com/en-us/windows/wsl/install-win10) for more information on WSL and the windows store options.

TODO: they need access to our ansible setup!!!

---

## Server access

Ansible uses ssh to communicate with the servers so you'll need to be able to access them from your shell directly.

The ideal way to achieve this is to setup key based authentication, however there are workarounds that can be done if you have to use password based authentication.

For more info on setting up an ssh private key, see [this tutorial](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)

As mentioned in the linked article, we will need to add each of our servers to our local list of known hosts, this is done by manually connecting to each of them for our shell.

    ssh -i path/to/keyfile <username>@<server_ip>
    e.g. ssh -i /home/nicky/.ssh/id_rsa nicky@10.10.10.1

---

## Config

Download [this hosts file](/assets/config/swarm.yml) and update the values as follows:

| Key                                   | Description                                                                                                                                                                                                                      |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| all.hosts.gateway.ansible_host        | IP For Gateway server accessible from your machine                                                                                                                                                                               |
| all.hosts.nfs_server.ansible_host     | IP For Gateway server accessible from your machine                                                                                                                                                                               |
| all.hosts.nfs_server.internal_ip      | internal IP For Gateway server, if you do not have an internal subnet, use the same IP as above                                                                                                                                  |
| all.hosts.manager(1,2,3).ansible_host | IP For Manager node accessible from your machine                                                                                                                                                                                 |
| all.hosts.manager(1,2,3).internal_ip  | internal IP For Manager node, if you do not have an internal subnet, use the same IP as above                                                                                                                                    |
| all.vars.ansible_user                 | Your username on all servers                                                                                                                                                                                                     |
| all.vars.ansible_ssh_private_key_file | Full path to your keyfile (leave blank if using password auth)                                                                                                                                                                   |
| all.vars.swarm_ip_mask                | ip mask that matches your internal subnet e.g. 10.10.10.10/24, or that matches all swarm nodes if you do not have an internal subnet                                                                                             |
| all.vars.ssl_certs                    | For ssl to work on your environment, you need to have a pem encoded certificate and keyfile for each domain you plan to serve on. You should name these files name.crt and name.key and then add all of the names in this field  |
| all.vars.dashboard_host               | The domain name for your portainer dashboard                                                                                                                                                                                     |
| all.vars.proxy_dashboard_host         | The domain name for your traefik proxy dashboard                                                                                                                                                                                 |
| all.vars.monitoring                   | This section will be covered in Advanced below, you should get the swarm up and running first before adding monitoring                                                                                                           |
| all.children                          | This section of the config file is for defining where your nodes will sit, please follow the instructions provided in the file itself, adding all nodes to the coreos group, and managers and workers to their respective groups |

---

## Deploy

1.  Save your config file in the hosts directory
1.  run the deploy playbook:

        ansible-playbook -i hosts/swarm.yml deploy.yml -v

---

## Update DNS records

Ensure that DNS records for your portainer dashbaord and traefik dashboard as defined in your config file are pointing to your Gateway server

---

## Portainer Setup

1.  Open Dashboard as defined in `{{dashboard_host}}` above

1.  Create admin user when prompted TODO: confirm this

1.  Add Dockerhub auth

    - Open Registries
    - Tick Authentication
    - add Username, Password

---

## Run Kudos Boards (and other apps) with Portainer

See [Kudos Boards for Docker Swarm](/boards/swarm/) for a step by step guide to running Kudos Boards on your new environment.

---

## Advanced (logging and monitoring)

TODO

## Troubleshooting

#### Recover from Cluster crash

Start new cluster

    docker swarm init --force-new-cluster --advertise-addr 10.142.0.12:2377

Check other Nodes automatically join new cluster

    docker node ls

If they don't, use the join command provided, ie:

    docker swarm join --token SWMTKN-1-1korweqob1x2530nc34uex84j03pa1e3x7qg5z2pt4bvt2fo5i-0aoijiczvso7socyzlrucbu8y 10.142.0.12:2377

List 'Down' nodes

    docker node ls

Remove 'Down' nodes

    docker node demote <node_id>
    docker node rm <node_id>

#### Recover from Service crash

- Run deploy stacks again
- Update each stack/service through Portainer

#### Rebalance containers on Nodes

    docker service update --force <stack>_<service>

ie:

    docker service update --force portainer_portainer proxy_proxy portainer_agent
