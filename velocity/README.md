# UrbanCode Velocity

Velocity brings reporting and analytics dashboard for UrbanCode Deploy.

## Pre-requisite

- Kubernetes 1.4+ with Beta APIs enabled
- Helm v2.6  (version might vary, which ever is compatible with your Kuberetes cluster).
- MongoDB with persistent volume. <https://github.com/kubernetes/charts/tree/master/stable/mongodb>
- Your UrbanCode Velocity license key. Get one for FREE from the UrbanCode Velocity registration site. <br/> http://di-kube.us-south.containers.mybluemix.net:32018/

## Installing the Chart and images

1. Get the required helm charts.

  ```sh
  $ helm init
  $ helm repo add urbancode https://raw.githubusercontent.com/skalmadka/urbancode-helm/master/repo
  $ helm fetch urbancode/velocity
  ```

2. Refer to the Configuration section below to customize the deployment. The following step (step 3) shows the values at minimal that are required to be set.

3. Deploy to your Kubernetes cluster.

  ```sh
  $ helm install \
    --set license.key=<velocity-license-key> \
    --set url.domain=<sub.domain.com> \
    --set mongo.url=mongodb://<mongo-username>:<mongo-password>@<mongo-service-name/URL>:27017/<database-name> \
    --set encrypt.key=<a-unique-guid/string-for-data-encryption> \
    --set adminpassword=admin \
    --name my-release urbancode/velocity
  ```

4. Read the NOTES section from the result of the previous command.

## Configuration

The following tables lists the configurable parameters of the Velocity chart and their default values.

Parameter                     | Description
----------------------------- | ---------------------------------------------------------------------------------------------------
license.key                   | Your Velocity license key. Get one for FREE from the UrbanCode Velocity registration site. <br/> http://di-kube.us-south.containers.mybluemix.net:32018/
prefixname                    | `velocity` A prefix to be added to all pods, services and ingress names. Limit to 20 characters.
url.protocol                  | `http` https not supported yet.
url.domain                    | This is usually the ingress host name or the hostname of your Kubernetes master node. <br/>  If you have any reverse proxy in front of your Kubernetes cluster, that becomes your domain. <br/> <b>Do not use IP address.</b>
mongo.url                     | `mongodb://<mongo-username>:<mongo-password>@<mongo-service-name/URL>:<mongo-port>/<database-name>`
encrypt.key                   | A unique id used to encrypt user names, tokens and any email addresses in mongoDB.
adminpassword                 | `admin`
consumer.image.repository     | velocity-conusmer image name.
consumer.image.tag            | velocity-conusmer image tag.
consumer.image.pullPolicy     | `Always`
consumer.service.type         | service type `ClusterIP`
consumer.service.externalPort | Maps internalPort to externalPort
ui.image.repository           | velocity-ui image name.
ui.image.tag                  | velocity-ui image tag.
ui.image.pullPolicy           | `Always`
ui.service.type               | service type `ClusterIP`
ui.service.externalPort       | Maps internalPort to externalPort
ingress.enabled               | `true` to enable ingress.

## Uninstalling the release

NOTE: this will remove all Velocity pod deployments, services and ingress rules (if enabled) that were installed on your Kube cluster as part of this release.

```sh
$ helm delete my-release
```
