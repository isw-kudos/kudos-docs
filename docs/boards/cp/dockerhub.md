## Moving from your local HCL Connections repository to Kudos Boards latest releases.

You can get the latest versions of Kudos Boards Docker by subscribing to our own repository in dockerhub as follows:

1. Create a dockerhub account if you do not already have one.
1. Email support@kudosapps.com requesting access to Kudos Boards Docker repository,include your dockerhub account name in the email.
1. Once confirmed by reply email update your config file as per [this example](/assets/config/kubernetes/boards-cp-dockerhub.yaml).
1. Create kubernetes secret with your dockerhub account credentials

    kubectl create secret docker-registry dockerhub --docker-server=docker.io --docker-username=[user] --docker-password=[password] --docker-email=[email] --namespace=connections

1. Run helm to apply the changes.

    helm upgrade kudos-boards-cp [PATH_TO_HELM_CHARTS]/kudos-boards-cp-1.0.0.tgz -i -f ./boards-cp.yaml --namespace connections --recreate-pods

