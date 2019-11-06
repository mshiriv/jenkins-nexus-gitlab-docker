# Jenkins, Nexus and GitLab docker compose

Run the latest version of Jenkins,  Nexus and GitLab with Docker Compose.
It gives you the ability to use GitLab as git repository, Jenkins as CI server and  Nexus to manage binaries and build artifacts across your software supply chain. 
Based on the official Docker images from Jenkins and Nexus :
* [Jenkins](https://github.com/jenkinsci/docker)
* [Nexus](https://github.com/sonatype/docker-nexus3)
* [Nginx](https://github.com/nginxinc/docker-nginx)

Also GitLab based on [Dockerized GitLab](https://github.com/sameersbn/docker-gitlab).

## Contents

1. [Requirements](#requirements)
   * [Host setup](#host-setup)
2. [Usage](#usage)
   * [Bringing up the stack](#bringing-up-the-stack)
   * [Cleanup](#cleanup)
3. [Configuration](#configuration)
   * [How to configure GitLab](#how-to-configure-GitLab)
   * [How to configure Nginx](#how-to-configure-Nginx)


## Requirements
### Host setup
* [Docker Engine](https://docs.docker.com/install/) 
* [Docker Compose](https://docs.docker.com/compose/install/)

By default, the stack exposes the following ports:
* 80: Nginx
* 10022: GitLab SSH 

And also you can access stack service, through docker network, following ports:
* 80: GitLab
* 8080: Jenkins
* 8081: Nexus

# Services Architecture
![picture](./services_architecture.jpg)

## Usage
### Bringing up the stack

Clone this repository, then start the stack using Docker Compose:
```console
$ docker-compose up
```
You can also run all services in the background (detached mode) by adding the `-d` flag to the above command.
> :information_source: You must run `docker-compose build` first whenever you switch branch or update a base image.
If you are starting the stack for the very first time, please read the section below attentively.

### Cleanup

In order to entirely shutdown the stack and remove all persisted data, use the following Docker Compose command:
```console
$ docker-compose down -v
```

## Configuration
> :information_source: Configuration is not dynamically reloaded, you will need to restart individual components after
any configuration change.
### How to configure GitLab
Please refer to the following documentation page for more details about how to configure GitLab inside Docker
containers: [Dockerized GitLab](https://github.com/sameersbn/docker-gitlab).
### How to configure Nginx
Nginx route requests to services using Nginx upstearm. The Nginx default configuration is stored in [`nginx/config/nginx.conf`].
Also you can change each service upstearm default configurtion stored in [`nginx/config/`]. For exapmle if you want change GitLab HTTP address,
you should change `GITLAB_HOST` on docker-compose, GitLab service, and also `server_name` on [`nginx/config/gitlab.conf`]