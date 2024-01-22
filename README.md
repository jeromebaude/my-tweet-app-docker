# my-tweet-app-docker 

![alt text](https://github.com/jeromebaude/my-tweet-app-docker/blob/main/app/static/ABC-2021-LOGO-small.jpg?raw=true)

Docker demo example application

## For what is this repository?

This application is designed to show how easy it is to build a Docker image and scan it with Docker Scout with Visual Studio Code and GitHub Actions.

It is using a simple Docker container image based on Alpine, Python and Flask as componentes that have some vulnerabilities.

## How can you use it?

To be able to use it you must have:

1. A Github account that you can use to fork this repository
2. Installation of Visual Studio Code on your local machine
3. A AWS EKS Kubernetes cluster
4. Your AWS access key that is allowed to manage the EKS cluster
5. A DockerHub account that can be used to save your images build via Github Actions


### Get Visual Studio Code up and running.

TBD
You can test it by executing a Task via Command+Shift+P and select one of the following:

It is important to use the right Task, as you otherwise might see some diffs between your local image scan and the scan of the Github Actions.

### Create an AWS EKS cluster for your runtime.

Before you can use the full Github Actions deployment you need to create an AWS EKS cluster, so we can deploy the application to. We highly recommend using eksctl to create it [https://eksctl.io/](.https://eksctl.io/) Please make sure that you have the access key and secret of the account that was used to create the EKS cluster.

### DockerHub account

For the Github Action task to be able to push the image that will be used by your kubernetes cluster you need to have a DockerHub account that can be used for the repositories.

### Starting the Github Action tasks.

The Github Actions tasks defined inside [docker.yml](.github/workflows) will be auto started as soon as you commit anything to your new Github repository. However to get it up and running you need to configure the following secrets inside your Github repository (Settings > Secrets):

* KUBE_CONFIG_DATA: KUBE_CONFIG_DATA – required: A base64-encoded kubeconfig file with credentials for Kubernetes to access the cluster. You can get it by running the following command:

cat $HOME/.kube/config | base64

* REGISTRY_USER: Your Dockerhub Username
* REGISTRY_TOKEN: Your Dockerhub access token
* AWS_ACCESS_KEY_ID: Your AWS Access Key ID that is allowed to use the EKS cluster.
* AWS_SECRET_ACCESS_KEY: Your AWS Secret Access Key that is allowed to use the EKS cluster.
