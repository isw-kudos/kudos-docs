# Activities Plus Install FAQ

If you are following the HCL install documentation, these notes need to be applied during the relevant sections. We recommend using our [install documentation](https://docs.kudosapps.com/boards/cp/) instead.

There are also some more [notes and insights](https://blog.msbiro.net/2020/02/hcl-connections-65-actity-plus-tips-setup.html) from one of our partners which is a great read.

## Installing Activities Plus services

<!-- - There is an [HCL Technote](https://support.hcltechsw.com/csm?id=kb_article&sysparm_article=KB0074334) (KB0074334) that needs to be followed -->

- Please use our [helm chart](/assets/config/kubernetes/kudos-boards-cp-1.1.1.tgz)
        <br>Note: if you are using Kubernetes below 1.13 use [this chart](/assets/config/kubernetes/kudos-boards-cp-1.0.0.tgz) instead.

- We recommend following the [Configuring the S3 storage mount](https://help.hcltechsw.com/connections/v65/admin/install/cp_3p_config_ap_s3_storage_mount.html) steps before running the helm upgrade command

- The helm upgrade command needs to be run from the directory containing boards-cp.yaml and the correct command is:

        helm upgrade kudos-boards-cp path_to_helm_charts/kudos-boards-cp-1.0.0-20191120-214007.tgz -i -f ./boards-cp.yaml --namespace connections --recreate-pods

    e.g.

        helm upgrade kudos-boards-cp /root/microservices_connections/hybridcloud/helmbuilds/kudos-boards-cp-1.0.0-20191120-214007.tgz -i -f ./boards-cp.yaml --namespace connections --recreate-pods

## Configuring IBM HTTP Server as reverse proxy

- If you do not have them enabled, you will need to enable the following modules by uncommenting them (remove the '#'):

        LoadModule proxy_module modules/mod_proxy.so
        LoadModule proxy_connect_module modules/mod_proxy_connect.so
        LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
        LoadModule proxy_http_module modules/mod_proxy_http.so

        LoadModule rewrite_module modules/mod_rewrite.so

- If you have not specified earlier (such as during other component-pack app installs), please set `ProxyPreserveHost On` before the Huddo Boards section in the VirtualHost

## Updating the Activities Plus configuration file

- Please use this [boards-cp.yaml](/assets/boards/cp/boards-cp.yaml) NOT the one supplied with the component pack.

## Migrating Activities data

- The helm upgrade command needs to be run from the directory containing boards-cp.yaml and the correct command is:

        helm upgrade kudos-boards-cp-activity-migration path_to_helm_charts/kudos-boards-cp-activity-migration-1.0.0-20191120-214007.tgz -i -f ./boards-cp.yaml --namespace connections --recreate-pods

    e.g.

        helm upgrade kudos-boards-cp-activity-migration /root/microservices_connections/hybridcloud/helmbuilds/kudos-boards-cp-activity-migration-1.0.0-20191120-214007.tgz -i -f ./boards-cp.yaml --namespace connections --recreate-pods
