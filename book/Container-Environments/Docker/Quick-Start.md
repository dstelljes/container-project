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
Obviously, containers can be used for much more than printing a whale saying "Hello World!"  This time, let's download the image before running it. We can use the ```docker pull``` command to do this.

```bash
$ docker pull fedora
```

This will download the latest version of the fedora image from Docker Hub. Let's spin up a fedora container with an interactive shell.

```bash
$ docker run -i -t fedora /bin/bash
[root@a58980471b84 /]#
```

As you can see, you are now root within an instance of fedora. What exactly did we call there, though?
* The ```-i``` flag starts an interactive container.
* The ```-t``` flag creates a pseudo-TTY which attaches *stdin* and *stdout*.

If you want to name your container, you can use the ```--name my-name``` flag. For example, spinning up a container titled *fedora-rocks*:

```bash
$ docker run -i -t --name fedora-rocks fedora /bin/bash
[root@a58980471b84 /]#
```

### Listing Containers

While your fedora container is running, open up another terminal. You can view your currently running containers by the following:
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
6dc092fe3cc5        fedora              "/bin/bash"         11 seconds ago      Up 8 seconds                            my-fedora
```

You may be wondering, "great, I can see my running containers! How about my stopped or old containers?" You can view those by using the ```-a``` flag:

```bash
$ docker ps -a
```

### Starting / Stopping Containers
Obviously, it is not useful to always have to keep a terminal open with your current container. You can start an already created container by passing its name to the start command:

```bash
$ docker start my-fedora
```

To run a command on a started container, use the ```docker exec``` command:

```bash
$ docker exec -i -t my-fedora /bin/bash
[root@6dc092fe3cc5 /]#
```

This launches an interactive terminal with our container just as when we used the  ```docker run``` command earlier. When we exit this terminal, however, the container will not stop unlike when we ran it earlier.

To stop the container, use the  ```docker stop``` command:

```bash
$ docker stop my-fedora
my-fedora
```

You can now confirm that the container has stopped by listing the active containers:
```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Congrats! You have successfully ran your first few docker containers.
