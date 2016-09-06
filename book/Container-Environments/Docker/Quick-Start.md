# Docker

## Quick Start

### Check Installation
To spin up a Docker container, make sure Docker is installed on the workstation you are using.

```bash
$ docker -v
Docker version 1.12.1, build 23cf638
```

### Run whalesay!
Remember the fun Linux command, ```cowsay```? Docker provides an introduction container image based on it. We will use this image to spin up our first container. To spin up containers, we use the ```docker run``` command. The command follows the following argument pattern:

```bash
$ docker run [image name] [...]
```

To spin up a whalesay container, run the following command:

```bash
$ docker run docker/whalesay cowsay 'Hello World!'
```

We are telling docker to run a the [docker/whalesay](https://hub.docker.com/r/docker/whalesay) container. It will search for this container locally. Since you have not run this image before, it will then search for it on [Docker Hub](https://hub.docker.com). This is a site that hosts repositories of images for spinning up containers. Docker will then download the needed image. We are then telling Docker to initially run the command ```cowsay 'Hello World'``` and it will return the output. The output looks as the following:

```bash
______________
< Hello World! >
--------------
   \
    \
     \     
                   ##        .            
             ## ## ##       ==            
          ## ## ## ##      ===            
      /""""""""""""""""___/ ===        
 ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~   
      \______ o          __/            
       \    \        __/             
         \____\______/  
```

### Running more
Obviously, containers can be used for much more than printing a whale saying "Hello World!"
