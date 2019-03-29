## Kudos Boards Cloud for Docker Swarm

Checklist and considerations before installation

## Servers

This solution is designed to be a lightweight, cloud-like setup running locally in your data centre. You should expect to configure a minimum of 4 very small servers, see [Swarm Installation](/swarm/#server-information) for a table showing the requirements.

## Existing Infrastructure

Kudos Boards for Docker Swarm is able to take advantage of existing services in your network, if you have any of the following and would like to take advantage of them, please ensure you have all relevant access documented.

| Service                   | Requirements                                                               |
| ------------------------- | -------------------------------------------------------------------------- |
| MongoDB                   | URL, username and password                                                 |
| S3 Storage                | URL, Bucket name, username and password                                    |
| NFS Server                | IP address or hostname, must be accessible to all swarm servers            |
| SNI Capable reverse proxy | admin access to proxy to configure all domains (see SSL Certificate below) |

## SSL Certificates / DNS

You will need to have certificates and DNS entries that cover the following domains:

> Replace `example.com` with your actual company domain

| Service    | Example domain         | DNS                                 |
| ---------- | ---------------------- | ----------------------------------- |
| Swarm      | swarm.example.com      | A record pointing to gateway server |
| Boards     | boards.example.com     | CNAME swarm.example.com             |
| Boards API | api-boards.example.com | CNAME swarm.example.com             |

## SSH Access

To perform the installation, you need to setup some config files on a local machine that has ssh access to the servers, you should ssh to each server manually before proceeding to ensure you have the relevant signatures in place.

## Authentication

Kudos Boards is designed to be integrated into your current user management system, before logging in you will need to configure OAuth for one of the following providers:

| Provider                     | Registration / Documentation                                                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| IBM Connections (on premise) | [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSYGQH_6.0.0/admin/admin/r_admin_common_oauth_manage_list.html) |
| IBM Connections Cloud        | [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSL3JX/admin/bss/topics/manage_custom_apps.html)                |
| Microsoft Office 365         | [Azure app registrations](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)                         |
| Google                       | [Google Console](https://console.developers.google.com/apis/credentials)                                                              |
| LinkedIn                     | [LinkedIn](https://www.linkedin.com/developers/apps)                                                                                  |
| Facebook                     | [Facebook developer centre](https://developers.facebook.com/apps/2087069981334024/fb-login/settings/)                                 |

## Dockerhub

Access to the images for kudos boards is provided through [dockerhub](https://hub.docker.com), please ensure that you have an account setup and have the credentials at hand for the install.

## Ansible

Kudos Boards installation uses [Red Hat Ansible](https://www.ansible.com/), please ensure this is installed and working prior to the install [Guide here](/tools/ansible/)
