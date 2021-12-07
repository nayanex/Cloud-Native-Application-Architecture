
# Introduction

[![Orchestrators For Managing Containers At Scale](https://img.youtube.com/vi/QhDHmFz0FG4/0.jpg)](https://www.youtube.com/watch?v=QhDHmFz0FG4)

Welcome to the Container Orchestration lesson!

Once a team has developed an application, the next phase is represented by the release process. This includes techniques for service packaging, containerization, and distribution. The end result of a product release is represented by a service that is deployed in a production environment and can be accessed by consumers.

In this lesson, we will discuss how an application can be packaged using Docker and released to a Kubernetes cluster.

![Container Orchestration lesson outline](https://video.udacity-data.com/topher/2020/December/5fe106e5_screen-shot-2020-12-21-at-12.34.03-pm/screen-shot-2020-12-21-at-12.34.03-pm.png)

Overall, in this lesson we will explore:

* Docker for Application Packaging
* Container Orchestration with Kubernetes
* Kubernetes Resources
* Declarative Kubernetes Manifests

# Transitions from VMs to Containers

[![Transitions From VMs To Containers](https://img.youtube.com/vi/2Ht4CGMh1qc/0.jpg)](https://www.youtube.com/watch?v=2Ht4CGMh1qc)

## VMs

In the past years, VMs (Virtual Machines) were the main mechanism to host an application. VMs encapsulate the code, configuration files, and dependencies necessary to execute the application.

![Multiple applications hosted on VMs](https://video.udacity-data.com/topher/2020/December/5fde3880_screenshot-2020-12-19-at-17.29.28/screenshot-2020-12-19-at-17.29.28.png)

In essence, a VM is composed of an **operating system** (OS) with a set of pre-installed libraries and packages. During execution, an **application** utilizes an OS filesystem, resources, and packages.

A set of VMs is managed through a **hypervisor**. A hypervisor provides the virtualization of the **infrastructure** which is composed of physical servers. As a result, a hypervisor is capable of creating, configuring, and managing multiple VMs on the available servers. For example, we are able to running applications A, B, and C on 3 separate VMs.

The utilization of VMs introduced standardization in infrastructure provisioning, in association with efficient use of available infrastructure. Instead of running an application per server, a hypervisor enables multiple VMs to run at the same time to host multiple applications. However, there is one downside to this mechanism: it is not efficient enough. For example, applications A, B, and C uses the same Operating System. Replicating an OS consumes a lot of resources, and the more applications we run the more space we allocate to the replication of the operating systems alone.

## Containers

![The transition from VMs to containers](https://video.udacity-data.com/topher/2020/December/5fde7a73_screenshot-2020-12-19-at-22.10.50/screenshot-2020-12-19-at-22.10.50.png)

There was a clear need to optimize the usage of the available infrastructure. As a result, the virtualization of the Operating System was introduced. This prompted the appearance of **containers**, which represent the bare minimum an application requires for a successful execution e.g. code, config files, and dependencies. By default, there is a better usage of available infrastructure.

Multiple VMs on a hypervisor are replaced by multiple containers running on a single host operating system. The processes in the containers are completely isolated but are able to access the OS filesystem, resources, and packages. The creation and execution of containers is delegated to a container management tool, such as Docker.

The appearance of containers is unlocked by OS-level virtualization and as a result, multiple applications can run on the same OS. By nature, containers are lightweight, as these encapsulate only the application code and essential dependencies. Consequently, there is a better usage of available infrastructure and a more efficient pathway to release a product to consumers.

# Docker for Application Packaging

[![Docker For Application Packaging](https://img.youtube.com/vi/ZGBhF9XtVDk/0.jpg)](https://www.youtube.com/watch?v=ZGBhF9XtVDk)

The appearance of containers enabled organizations to ship products using a lightweight mechanism, that would make the most of available infrastructure. There are plenty of tools used to containerize services, however, Docker has set the industry standards for many years.

To containerize an application using Docker, 3 main components are distinguished: Dockerfiles, Docker images, and Docker registries. Let's explore each component in a bit more detail!

## Dockerfile

A Dockerfile is a set of instructions used to create a Docker image. Each instruction is an operation used to package the application, such as installing dependencies, compile the code, or impersonate a specific user. A Docker image is composed of multiple layers, and each layer is represented by an instruction in the Dockerfile. All layers are cached and if an instruction is modified, then during the build process only the changed layer will be rebuild. As a result, building a Docker image using a Dockerfile is a lightweight and quick process.

To construct a Dockerfile, it is necessary to use the pre-defined instructions, such as:

```Dockerfile
FROM -  to set the base image
RUN - to execute a command
COPY & ADD  - to copy files from host to the container
CMD - to set the default command to execute when the container starts
EXPOSE - to expose an application port 
```

Below is an example of a Dockerfile that targets to package a Python hello-world application:

```Dockerfile
# set the base image. Since we're running 
# a Python application a Python base image is used
FROM python:3.8
# set a key-value label for the Docker image
LABEL maintainer="Katie Gamanji"
# copy files from the host to the container filesystem. 
# For example, all the files in the current directory
# to the  `/app` directory in the container
COPY . /app
#  defines the working directory within the container
WORKDIR /app
# run commands within the container. 
# For example, invoke a pip command 
# to install dependencies defined in the requirements.txt file. 
RUN pip install -r requirements.txt
# provide a command to run on container start. 
# For example, start the `app.py` application.
CMD [ "python", "app.py" ]
```

## Docker Image

[![Docker Image](https://img.youtube.com/vi/QqSaf8xogh0/0.jpg)](https://www.youtube.com/watch?v=QqSaf8xogh0)

Once a Dockerfile is constructed, these instructions are used to build a **Docker image**. A Docker image is a read-only template that enables the creation of a runnable instance of an application. In a nutshell, a Docker image provides the execution environment for an application, including any essential code, config files, and dependencies.

A Docker image can be built from an existing Dockerfile using the `docker build` command. Below is the syntax for this command:

```Dockerfile
# build an image
# OPTIONS - optional;  define extra configuration
# PATH - required;  sets the location of the Dockefile and  any referenced files 
docker build [OPTIONS] PATH

# Where OPTIONS can be:
-t, --tag - set the name and tag of the image
-f, --file - set the name of the Dockerfile
--build-arg - set build-time variables

# Find all valid options for this command 
docker build --help
```

For example, to build the image of the Python hello-world application from the Dockerfile, the following command can be used:

```Dockerfile
# build an image using the Dockerfile from the current directory
docker build -t python-helloworld .

# build an image using the Dockerfile from the `lesson1/python-app` directory
docker build -t python-helloworld lesson1/python-app
```

Before distributing the Docker image to a wider audience, it is paramount to test it locally and verify if it meets the expected behavior. To create a container using an available Docker image, the `docker run` command is available. Below is the syntax for this command:

```Dockerfile
# execute an image
# OPTIONS - optional;  define extra configuration
# IMAGE -  required; provides the name of the image to be executed
# COMMAND and ARGS - optional; instruct the container to run specific commands when it starts 
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

# Where OPTIONS can be:
-d, --detach - run in the background 
-p, --publish - expose container port to host
-it - start an interactive shell

# Find all valid options for this command 
docker run --help
```

For example, to run the Python hello-world application, using the created image, the following command can be used:

**Note**: To access the application in a browser, we need to bind the Docker container port to a port on the host or local machine. In this case, `5111` is the host port that we use to access the application e.g. `http://127.0.0.1:5111/`. The `5000` is the container port that the application is listening to for incoming requests.

```Dockerfile
# run the `python-helloworld` image, in detached mode and expose it on port `5111`
docker run -d -p 5111:5000 python-helloworld
```

To retrieve the Docker container logs use the `docker logs {{ CONTAINER_ID }}` command. For example:

```Dockerfile
docker logs 95173091eb5e

## Example output from a Flask application
 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
```

## Docker Registry

[![Docker Registry](https://img.youtube.com/vi/kldYqVSB23E/0.jpg)](https://www.youtube.com/watch?v=kldYqVSB23E)

The last step in packaging an application using Docker is to store and distribute it. So far, we have built and tested an image on the local machine, which does not ensure that other engineers have access to it. As a result, the image needs to be pushed to a **public Docker image registry**, such as DockerHub, Harbor, Google Container Registry, and many more. However, there might be cases where an image should be private and only available to trusted parties. As a result, a team can host private image registries, which provides full control over who can access and execute the image.

Before pushing an image to a Docker registry, it is highly recommended to tag it first. During the build stage, if a tag is not provided (via the `-t` or `--tag` flag), then the image would be allocated an ID, which does not have a human-readable format (e.g. 0e5574283393). On the other side, a defined tag is easily scalable by the human eye, as it is composed of a registry repository, image name, and version. Also, a tag provides version control over application releases, as a new tag would indicate a new release.

To tag an existing image on the local machine, the `docker tag` command is available. Below is the syntax for this command:

```Dockerfile
# tag an image
# SOURCE_IMAGE[:TAG]  - required and the tag is optional; define the name of an image on the current machine 
# TARGET_IMAGE[:TAG] -  required and the tag is optional; define the repository, name, and version of an image
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

For example, to tag the Python hello-world application, to be pushed to a repository in DockerHub, the following command can be used:

```Dockerfile
# tag the `python-helloworld` image, to be pushed 
# in the `pixelpotato` repository, with the `python-helloworld` image name
# and version `v1.0.0`
docker tag python-helloworld pixelpotato/python-helloworld:v1.0.0
```
Once the image is tagged, the final step is to push the image to a registry. For this purpose, the `docker push` command can be used. Below is the syntax for this command:

```Dockerfile
# push an image to a registry 
# NAME[:TAG] - required and the tag is optional; name, set the image name to be pushed to the registry
docker push NAME[:TAG]
```

For example, to push the Python hello-world application to DockerHub, the following command can be used:

```Dockerfile
# push the `python-helloworld` application in version v1.0.0 
# to the `pixelpotato` repository in DockerHub
docker push pixelpotato/python-helloworld:v1.0.0
```

### New terms

* **Dockerfile** - set of instructions used to create a Docker image
* **Docker image** - a read-only template used to spin up a runnable instance of an application
* **Docker registry** - a central mechanism to store and distribute Docker images

### Further reading

Explore Dockerfiles best practices and valid list of instructions:

* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/#from)
* [Best practices for writing Dockerfiles](Best practices for writing Dockerfiles)

Explore how to build and run a Docker image, with a list of all available options:

* [Docker Build command](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker Run command](https://docs.docker.com/engine/reference/commandline/build/)

Explore Docker registries, alternatives to package an application, and OCI standards:

* [Introduction to Docker registry](https://docs.docker.com/registry/introduction/)
* [Docker Tag command](https://docs.docker.com/engine/reference/commandline/tag/)
* [Docker Push command](https://docs.docker.com/engine/reference/commandline/push/)
* [Demystifying the Open Container Initiative (OCI) Specifications](https://www.docker.com/blog/demystifying-open-container-initiative-oci-specifications/)
* [Buildpacks: An App’s Brief Journey from Source to Image](https://buildpacks.io/docs/app-journey/)

# Docker Walkthrough

This demo provides a step-by-step walkthrough of how to package, build, run, tag, and push a Docker image. You can follow this demo by referencing the Dockerfile from the course repository.

[![Docker Registry](https://img.youtube.com/vi/kldYqVSB23E/0.jpg)](https://www.youtube.com/watch?v=RWClSVNEGIg)

# Useful Docker Commands

Docker provides a rich set of actions that can be used to build, run, tag, and push images. Below is a list of handy Docker commands used in practice.

**Note**: In the following commands the following arguments are used:

**OPTIONS** - define extra configuration through flags
**IMAGE** - sets the name of the image
**NAME**- set the name of the image
**COMMAND** and **ARG** - instruct the container to run specific commands associated with a set of arguments

## Build Images

To build an image, use the following command, where PATH sets the location of the Dockerfile and referenced application files:

```Dockerfile
docker build [OPTIONS] PATH
```

## Run Images
To run an image, use the following command:

```Dockerfile
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

## Get Logs

To get the logs from a Docker container, use the following command:

```Dockerfile
docker logs CONTAINER_ID 
```

Where the CONTAINER_ID is the ID of the Docker container that runs an application.

## List Images

To list all available images, use the following command:

```Dockerfile
docker images 
```

## List Containers

To list all running containers, use the following command:

```Dockerfile
docker ps 
```

## Tag Images

To tag an image, use the following command, where SOURCE_IMAGE defines the name of an image on the current machine and TARGET_IMAGE defines the repository, name, and version of an image:

```Dockerfile
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG] 
```

## Login to DockerHub

To login into DockerHub, use the following command:

```Dockerfile
docker login 
```

## Push Images

To push an image to DockerHub, use the following command:

```Dockerfile
docker push NAME[:TAG] 
```

## Pull Images

To pull an image from DockerHub, use the following command:

```Dockerfile
docker pull NAME[:TAG]
```

# Quizzes: Docker for Application Packaging

## QUESTION 1 OF 3

Match the following Docker components with their main functionality:

DOCKER COMPONENT | PURPOSE
---------------------------
Dockerfile | Set of instructions to create a Docker image
Docker image | A read-only template that is used spin up a container
Docker container | A runnable instance of the Docker image 
Docker registry | A tool used to store and distribute Docker images

## QUESTION 2 OF 3

By default, Docker will create OCI (Open Container Initiative) compliant images. What is the reason for using OCI guidelines?

[ ] To ensure everyone uses Docker
[x] To standardize the image formats 
[x] To ensure that images can execute on OCI compliant runtime
[ ] To ensure Dockerfiles are used as a standard component 

## QUESTION 3 OF 3

What is the Docker command used to get the following output?

DOCKER COMMAND | OUTPUT
-------------------------
Build a Docker image using `Dockerfile.staging` file in the `app/backend` folder | `docker build \ - f Dockerfile.staging app/backend`
Create an interactive shell to a `busybox` container | `docker run -it  busybox`
Tag the new image ID as the front-end application in version `v4.5.2`| `docker tag  f10f0a406345 \pixelpotato/frontend:v4.5.2`
Push the new front-end application to DockerHub | `docker push  \pixelpotato/frontend:v4.5.2`
Login into the DockerHub using valid credentials | `Docker login`

### Get deployments
`kubectl get deploy`

### Get Replicas
`kubectl get rs`

### Get Pods
`kubectl get po`

`kubectl get po -n test-udacity`

### Get Nodes
`kubectl get no`

### Get ConfigMaps
`kubectl get cm`

### Get Secrets
`kubectl get secrets`

### Create Deployment
`kubectl create deploy go-helloworld --image=pixelpotato/go-helloworld:v1.0.0`

`kubectl port-forward po/go-hellowworld-fcd468f98-zjvlg 6111:6111`

> Where go-hellowworld-fcd468f98-zjvlg is the name of the pod which host the container
> You can access the application going to 127.0.0.1:6111

### Edit deployment
`kubectl edit deploy go-helloworld -o yaml`

> You can, for example, change the image version

### Deleting a namespace
`kubectl delete namespaces <insert-some-namespace-name>`

### Create a namespace
`kubectl create ns demo --dry-run=client -o yaml > namespace.yaml`

### Label a resource
`kubectl label deploy nginx-alpine tag=alpine --namespace demo`

`kubectl label ns demo tier=test`

### create the nginx-alpine deployment 
`kubectl create deploy nginx-alpine --image=nginx:alpine  --replicas=3 --namespace demo`

### label the deployment
`kubectl label deploy nginx-alpine app=nginx tag=alpine --namespace demo`

### expose the nginx-alpine deployment, which will create a service
`kubectl expose deployment nginx-alpine --port=8111 --namespace demo`

> expose the `go-helloworld` deployment on port 8111

### note: the application is serving requests on port 6112
`kubectl expose deploy go-helloworld --port=8111 --target-port=6112`

`kubectl run test-$RANDOM --namespace=default --rm -it --image=alpine -- sh`

`wget -qO- 10.98.151.167:6112 `

### create a config map
`kubectl create configmap nginx-version --from-literal=version=alpine --namespace demo`

### create a Configmap to store the color value
`kubectl create configmap test-cm --from-literal=color=yellow`

### create a Secret to store the secret color value
`kubectl create secret generic test-secret --from-literal=color=blue`

`kubectl describe secrets test-secret`

`kubectl get secrets test-sec -o yaml`

`echo "cmVk" | base64 -D`

### Get Logs
`kubectl logs RESOURCE/NAME [FLAGS]`

### Delete Resources
`kubectl delete RESOURCE NAME`
