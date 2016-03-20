---
layout: default
title: Installing JHipster
permalink: /installation/
redirect_from:
  - /installation.html
sitemap:
    priority: 0.7
    lastmod: 2014-02-17T00:00:00-00:00
---

# <i class="fa fa-cloud-download"></i> Installing JHipster

## Installation types

We provide 3 ways of working with JHipster:

*   A "local installation", which is the classical way of working with JHipster. Everything is installed on your machine, which can be a little complex to set up, but that's how most people usually work. In case of doubt, choose this installation.
*   A Vagrant-based "[development box](https://github.com/jhipster/jhipster-devbox)", with all tools already set up in a Ubuntu-based virtual machine.
*   A "[Docker](https://www.docker.io/)" container, which brings you a lightweight, virtualized container with JHipster installed.

## Local installation (recommended for normal users)

1.  Install Java 8 from [the Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2.  (Optional) Install a Java build tool.
    *   Whether you choose to use [Maven](http://maven.apache.org/) or [Gradle](http://www.gradle.org/), you normally don't have to install anything, as JHipster will automatically install the [Maven Wrapper](https://github.com/takari/maven-wrapper) or the [Gradle Wrapper](http://gradle.org/docs/current/userguide/gradle_wrapper.html) for you.
    *   If you don't want to use those wrappers, go to the official [Maven webiste](http://maven.apache.org/) or [Gradle website](http://www.gradle.org/) to do your own installation.
3.  Install Git from [git-scm.com](http://git-scm.com/). We recommend you also use a tool like [SourceTree](http://www.sourcetreeapp.com/) if you are starting with Git.
4.  Install Node.js from [the Node.js website](http://nodejs.org/). This will also install `npm`, which is the node package manager we are using in the next commands.
5.  Install Yeoman: `npm install -g yo`
6.  Install Bower: `npm install -g bower`
7.  Install Gulp: `npm install -g gulp`
8.  Install JHipster: `npm install -g generator-jhipster`

To find more information, tips and help, please have a look at [the Yeoman "getting starting" guide](http://yeoman.io/learning/index.html) and at the [NPM documentation](https://docs.npmjs.com/) before [submitting a bug](https://github.com/jhipster/generator-jhipster/issues?state=open).

Now that JHipster is installed, your next step is to [create an application]({{ site.url }}/creating-an-app/)

## Vagrant box installation

The [JHipster development box](https://github.com/jhipster/jhipster-devbox) project gives you a virtual machine with all the necessary tools to develop your JHipster project.

It's an easy way to get up and running very quickly with JHipster.

Besides JHipster, this virtual machine includes many development tools like the Spring Tool Suite, the Atom text editor and MySQL Workbench.

Please go to the [JHipster development box page](https://github.com/jhipster/jhipster-devbox) for installation and configuration information.

## Docker installation (for advanced users only)

_Please note: this Docker image is for running the JHipster generator inside a container. It's completely different from the [Docker and Docker Compose configurations]({{ site.url }}/docker-compose/) that JHipster will generate, which goal is to run your generated application inside a container_

### Information

JHipster has a specific [jhipster-docker project](https://github.com/jhipster/jhipster-docker), which provides a [Docker](https://www.docker.io/) container.

This project makes a Docker "Trusted build" that is available on:

[https://hub.docker.com/r/jdubois/jhipster-docker/](https://hub.docker.com/r/jdubois/jhipster-docker/)

This image will allow you to run JHipster inside Docker.

### Prerequisites

This depends on your operating system.

1.  **Linux:** Linux supports Docker out-of-box. You just need to follow the tutorial on the [Docker](https://docs.docker.com/installation/#installation) website.
2.  **Mac & Windows:** install the [Docker Toolbox](https://www.docker.com/docker-toolbox) to get Docker installed easily.

**Please note:** based on your OS your `DOCKER_HOST_IP` will differ. On Linux, it will be simply your localhost. For Mac/Windows, you will have to obtain the IP using following command: `docker-machine ip default`

As the generated files are in your shared folder, they will not be deleted if you stop your Docker container. However, if you don't want Docker to keep downloading all the Maven and NPM dependencies every time you start the container, you should commit its state.

<div class="alert alert-info"><i>Tip: </i>

Kitematic is an easy-to-use graphical interface provided with the Docker Toolbox, which will makes this installation a lot easier.

</div>

### Usage on Linux/Mac Windows (using Docker Toolbox)

#### Pull the image

Pull the JHipster Docker image:

`docker pull jdubois/jhipster-docker`

#### Run the image

Create a "jhipster" folder in your home directory:

`mkdir ~/jhipster`

Run the Docker image, with the following options:

*   The Docker "/home/jhipster/app" folder is shared to the local "~/jhipster" folder
*   Forward all ports exposed by Docker (8080 for Tomcat, 9000 for BrowserSync from the "gulp serve" task, 3001 for the BrowserSync UI)

`docker run --name jhipster -w /home/jhipster/app -v ~/jhipster:/home/jhipster/app:rw -v ~/.m2:/home/jhipster/.m2:rw -p 8080:8080 -p 9000:9000 -p 3001:3001 -d -t jdubois/jhipster-docker`

<div class="alert alert-info"><i>Tip: </i>

If you have already started the container once before, you do not need to run the above command, you can simply start/stop the existing container.

</div>

#### Check if the container is running

To check that your container is running, use the command `docker ps`:

`CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
4ae16c0539a3 jdubois/jhipster-docker "tail -f /home/jhipst" 4 seconds ago Up 3 seconds 0.0.0.0:9000-3001->9000-3001/tcp, 0.0.0.0:8080->8080/tcp **jhipster**`

#### Common operations

*   To stop the container execute: `docker stop jhipster`
*   And to start again, execute: `docker start jhipster`

In case you update the Docker image (rebuild or pull from the Docker hub), it's better to remove the existing container, and run the container all over again. To do so, first stop the container, remove it and then run it again:

1.  `docker stop jhipster`
2.  `docker rm jhipster`
3.  `docker pull jdubois/jhipster-docker`
4.  `docker run --name jhipster -w /home/jhipster/app -v ~/jhipster:/home/jhipster/app:rw -v ~/.m2:/home/jhipster/.m2:rw -p 8080:8080 -p 9000:9000 -p 3001:3001 -d -t jdubois/jhipster-docker`

On Linux, you might need to run the `docker` command as root user if your user is not part of docker group. It's a good idea to add your user to docker group so that you can run docker commands as a non-root user. Follow the steps on [http://askubuntu.com/a/477554](http://askubuntu.com/a/477554) to do so.

### Accessing the container

The easiest way to log into container is by executing following command:

`docker exec -it --user=jhipster <container_name> bash`

if you copy-pasted command to run container from above, notice the name being specified as jhipster

`docker exec -it --user=jhipster jhipster bash`

You will login as "jhipster" user. In case you need to do a `sudo`, password for the user is the same as the username (`jhipster`).

### Your first project

You can then go to the /home/jhipster/app directory in your container, and start building your app inside Docker:

`cd /home/jhipster/app`

`yo jhipster`

Once your application is created, you can run all the normal gulp/bower/maven commands, for example:

`mvn`

**Congratulations! You've launched your JHipster app inside Docker!**

On your host machine, you should be able to :

*   Access the running application at `http://DOCKER_HOST_IP:8080`
*   Get all the generated files inside your shared folder
