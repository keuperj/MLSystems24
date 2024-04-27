# Assignment 2: Docker

**Note:** for this assignment we use the bwLehrPool infrastructure. Boot the lab PC and start the ***XFCE Base Linux***.

## Links
* [Docker Reference](https://docs.docker.com/reference/)
* [Docker Hub](https://hub.docker.com/)
* [NVIDIA NGC](https://catalog.ngc.nvidia.com/containers)

## Basics
* Start a terminal and check the docker installation:
```
docker --version
```

* Check for running containers:
```
docker ps
```

* List localy available *images*:
```
docker images
```


### Tasks
#### Run your first container:
```
docker run hello-world
```
* Check local *images* again... what happend? 

#### Get a *Jupyter* and *Scikit-Learn* container running
* find a suitable image on *Docker Hub*
* pull the image
* start the container and open ```localhost:8888``` in your browser (Port my vary depending on the image you use)
* open a second terminal and check the state of running containers ```docker ps``` -> get the current container *ID*
* stop the container
* delete the image from the system

## Storage
Everything we store/save inside the container will be lost when the container terminates. Hence we want to mount persitent storage.

* [Bind-mount Docu](https://docs.docker.com/storage/bind-mounts/)

### Tasks
* create a folder in you home and mount it into the container *jupyter* container at start time. 
* create a new file in *Jupyter*, then terminate the container. Check if the file is still there at re-start.

## Network
*Jupyter* is a web-service. The start command you used, mapped some port of the cointainer (probably ```8888```) to a port of the host machine. But, this port might be already taken!

* [Network Docu](https://docs.docker.com/network/bridge/)

### Tasks
* Use the *publish* flag to map the *Jupyter* port in the container to port ```8856``` of the host and check the connection. 
* Keep the container running, execute ```docker ps``` one more time

## Changing Images
Now, we want to save changes made in the container

* [Docker commit docu](https://docs.docker.com/engine/reference/commandline/commit/)
* [Docker history](https://docs.docker.com/engine/reference/commandline/history/)

### Tasks
* go to *Jupyter* and install some software (*pip install ....*) and add a file in the container ```test.md```
* user ```docker commit``` to create a new image from the current state of the running container (Hint: you need the container ID)
* stop the current container 
* check for your new *image* and show the layer *history*
* start your new image and check if all the changes are there


## Building Images
Now, we want to build a new image from scratch, using a *Dockerfile*:
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

### Tasks
* follow the [example](https://docs.docker.com/language/python/build-images/) and create your own python image with a *Dokerfile*

