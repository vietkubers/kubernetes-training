## Docker Overview 

A solution to software deployment, Docker wraps everything that belongs to a software in a complete filesystem, code, runtime, system tools, system libraries, in a neat little package called an image. An image is created using a Dockerfile - a file that contains commands users could call on to build images. Each running instance of an image is called a container, each of which is isolated from one another and from the underlying infrastructure. An application can be composed of a single process running in a Docker container or it could be made up of multiple processes running in their own containers and being replicated as the load increases. Containers could communicate with one another through networking, or multiple containers could work together using Docker Compose. 

### Docker architecture

![Docker architecture](Docker_Architecture.png)

#### How Docker images are created 

Docker images could be created by running ```docker commit``` and ```docker save```, but since we want to automate the image creation process, we utilize a text file call Dockerfile, which combines all commands to create and build an image. Each command creates a read-only layer of the current image, therefore each layer is a delta change of the layer below it. 

Docker builds images automatically by reading the instructions from a Dockerfile. A Dockerfile adheres to a specific format and set of instructions which you can find at Dockerfile reference. So basically, what we learn in this section is to write Dockerfiles. 

Dockerfile is simply a file with commands on each line, each command written in the form ```INSTRUCTION arguments```. Everytime we run a command, we add a static layer to the image. 

Consider this Dockerfile: 

```sh
# our base image
FROM alpine:3.5

ENV http_proxy=http://10.164.177.170:8080
ENV https_proxy=http://10.164.177.170:8080

# Install python and pip
RUN apk add --update py2-pip

# upgrade pip
RUN pip install --upgrade pip

# install Python modules needed by the Python app
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# copy files required for the app to run
COPY app.py /usr/src/app/ 

#this could be more efficient by copying both app.py and requirements.txt into the same folder

COPY templates/index.html /usr/src/app/templates/

# tell the port number the container should expose
EXPOSE 5000

# run the application
CMD ["python", "/usr/src/app/app.py"]
```

Now, let's break it down to see each component of the Dockerfile. 

1. Creating a base image

A Dockerfile starts from the base image, or the platform dependencies required by your application. Here, we use nginx's alpine version 3.5 as a web platform for our flask app, so alpine:3.5 is the base image. 

```sh
# our base image
FROM alpine:3.5
```

2. Installing dependency packages 

In the next steps, we need to run a few commands to configure our image. One of those are ```COPY``` and ```RUN```. ```COPY``` creates a replica of the files in the current directory in a directory within the container (which is useful for source code and assets that you want to be deployed inside your container). ```RUN``` executes a command as it would be executed in the command prompt. This is used when we want to have any package installed or run a build command. 

```sh
# Install python and pip
RUN apk add --update py2-pip

# upgrade pip
RUN pip install --upgrade pip

# install Python modules needed by the Python app
COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r /usr/src/app/requirements.txt

# copy files required for the app to run
COPY app.py /usr/src/app/ 

#this could be more efficient by copying both app.py and requirements.txt into the same folder

COPY templates/index.html /usr/src/app/templates/
```

#### Dockerfile's best practice

While it is important to have a running container, it is no less important to create images that are efficient and well layered (see what I did there?). After we learn a language's syntax, it's best to know its recommended coding style. The same applies with Docker when we try to build images. 


##### Docker image sharing 

After running containers, we have some changes/new layers added to the base image. We want to keep these changes and maybe share them with others. Docker sharing is made for this task. We may want to store images on Dockerhub, a repository hosting website like github, or in our local registry - a place configured through web ports to store docker images.  

1. Docker registry 

### Docker Compose

####Compose file reference

### Docker Networking

### Docker Storage





