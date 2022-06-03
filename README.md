# jenkins-docker-deploy
A Jenkins shared library for deploying to a remote host via SSH

### Motive

In most cases, a delivery task is needed in order to deliver docker image to the remote host and then deploy the image through `docker run` command.
Aim of this project is to automate delivery and deployment of docker container to the remote host.

### Pre-requisites

You need to configure
* SSH Credentials on your jenkins controller (A server which you've deployed your Jenkins)
* Add your public key (e.g., `id_rsa.pub` or `id_dsa.pub`) to the `authorized_keys` to the deployment server.
* Install SSH agent plugin on your Jenkins
* Configure the library in your Jenkins installation

### Using the shared library

In your Jenkins, use the library as following

```jenkins
// Declarative pipeline
@Library('<name from your jenkins>') _

pipeline {
  stages {
  
    environment {
      DOCKER_IMG = "<Your image here>"
      SSH_HOST = "<Your Target server here>"
      SSH_USER = "<Your SSH User here>"
    }
  
    stage("Deploy") {
      // This will push the image `env.DOCKER_IMG` to the deployment host
      dockerRemoteSave(img: env.DOCKER_IMG, host: env.SSH_HOST, user: SSH_USER)
    }
  }
}
```
