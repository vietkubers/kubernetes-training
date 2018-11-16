## Docker Overview 

A solution to software deployment, Docker wraps everything that belongs to a software in a complete filesystem, code, runtime, system tools, system libraries, in a neat little package called an image. An image is created using a Dockerfile - a file that contains commands users could call on to build images. Each running instance of an image is called a container, each of which is isolated from one another and from the underlying infrastructure. An application can be composed of a single process running in a Docker container or it could be made up of multiple processes running in their own containers and being replicated as the load increases. Containers could communicate with one another through networking, or multiple containers could work together using Docker Compose. 

### Docker architecture

![Docker architecture](Docker_Architecture.png)

### Dockerfile image creation and sharing

After running containers, we have some changes/new layers added to the base image. We want to keep these changes and maybe share them with others. Docker image creation and sharing are made for these tasks. We can save each change to a container with docker commit and docker save, but we want to be able to automate the image creation process through a text file called Dockerfile. 

Dockerfile is simply a file with commands on each line, each command written in the form ```sh INSTRUCTION arguments```. Everytime we run a command, we build the image with a static layer. 

Using the flask-app example:

```sh
FROM alpine:3.5
```

#### 1. Creating a base image

A Dockerfile starts from the base image, or the platform dependencies required by your application. 

Example: 

A flask-app has nginx's alpine as its platform dependency, so we have alpine:3.5 as the base image

```sh
#set alpine:3.5 as the base image
FROM alpine:3.5
```

#### 2. Build image with RUN, COPY

In the next steps, we need to run a few commands to configure our image. One of those are ```COPY``` and ```RUN```. ```COPY``` creates a replica of the files in the current directory in a directory within the container (which is useful for source code and assets that you want to be deployed inside your container). ```RUN``` executes a command as it would be executed in the command prompt. This is used when we want to have any package installed or run a build command. 

```sh
#install python and pip
RUN apk add --update py2-pip
```
#### 3. Connect the app with outside world with EXPOSE

#### 4. Run application when container launches with CMD
CMD 

#### Dockerfile's best practice


### Docker Compose

####Compose file reference

### Docker Networking

### Docker Storage





