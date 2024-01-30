# my-tweet-app-docker 

![alt text](https://github.com/jeromebaude/my-tweet-app-docker/blob/main/app/static/ABC-2021-LOGO-small.jpg?raw=true)

Docker demo application

## For what is this repository?

This application is designed to show how easy it is to build a Docker image and scan it with Docker Scout using  GitHub Actions.

It is using a simple Docker container image based on Alpine, Python and Flask as components that have some vulnerabilities.

We are going to build a new Docker image and compare it with our production image. 

Docker Scout will tell us if the new image complies with our security requirements.

The production image is stored in DockerHub: index.docker.io/jeromebaude/my-tweet-app-docker:production

## How can you use it?

To be able to use it you must have:

1. A Github account that you can use to fork this repository
2. Installation of Visual Studio Code on your local machine
3. Docker Desktop 
4. A DockerHub account with Docker Scout enabled


### Build your image locally

Please update your Dockerfile with Dockerfile.vuln content and ./app/requirements.txt with ./app/requirements.txt.vuln content

Run the following commands:
```
docker build -t jeromebaude/my-tweet-app-docker:v1 .
```

### Run your image locally

Run the following commands:
```
docker run -d -p 5000:5000  jeromebaude/my-tweet-app-docker:v1
```

Check that http://localhost:5000 renders the desire look and feel

### Check your image vulnerabilities

Check the vulnerabilities of your newly built image
```
 docker scout quickview
```

Compare the new image vulnerabilities with your production image
```
 docker scout compare --to jeromebaude/my-tweet-app-docker:production jeromebaude/my-tweet-app-docker:v1
```

### Push your changes to your remote GitHub repo and run GitHub Actions

The Github Actions tasks defined inside [docker.yml](.github/workflows) will be auto started as soon as you commit anything to your new Github repository. However to get it up and running you need to configure the following secrets inside your Github repository (Settings > Secrets):

* REGISTRY_USER: Your Dockerhub Username
* REGISTRY_TOKEN: Your Dockerhub access token

Commit and push changes to the remote repo:
```
 git add Dockerfile ./app/requirements.txt
 git commit -m "updating my Docker image to be built"
 git push
```
You can check your GitHub Action Workflow and adapt it according to your needs.

### Clean your environment

```
 docker rm -f $(docker ps -a -q)
 cp ./app/requirements.txt.vuln ./app/requirements.txt
 cp Dockerfile.vuln Dockerfile 
```
