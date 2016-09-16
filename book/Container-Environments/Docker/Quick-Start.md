# Docker Quick Start

## Install Docker

Before you can spin up your first Docker container, Docker has to be installed on the workstation you are using:

```bash
$ docker -v
Docker version 1.12.1, build 23cf638
```

If you don’t have Docker installed, [the installation guide](https://docs.docker.com/engine/installation/) has instructions for most common operating systems.

To create containers, the Docker daemon must be running. A quick way to check that is try to list containers -- it will give back an error if it is not running:

```bash
$ docker ps
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

If you receive an error as shown above, the Docker daemon is not running and containers can not be created. The service will have to be started before you can continue. If you got an empty list, the daemon is running and we're ready to continue!

## Run `whalesay`

Remember the fun Linux command `cowsay`? Docker provides an introduction container image based on it. We will use this image to spin up our first container. To spin up containers, we use the `docker run` command. The command follows the following pattern:

```bash
$ docker run [image name] [...]
```

To spin up a `whalesay` container, run the following command:

```bash
$ docker run docker/whalesay cowsay 'Hello World!'
```

We are telling docker to run a the [`docker/whalesay`](https://hub.docker.com/r/docker/whalesay) container. It will search for this container locally. Since you have not run this image before, it will then search for it on [Docker Hub](https://hub.docker.com). This is a site that hosts repositories of images for spinning up containers. Docker will then download the needed image. We are then telling Docker to initially run the command `cowsay 'Hello World'` and print the output:

```
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

## Run Fedora

Obviously, containers can be used for much more than printing a whale saying “Hello World!”  This time, let’s download the image before running it. We can use the `docker pull` command to do this:

```bash
$ docker pull fedora
```

This will download the latest version of the Fedora image from Docker Hub. Let’s spin up a Fedora container with an interactive shell:

```bash
$ docker run -i -t fedora /bin/bash
[root@a58980471b84 /]#
```

As you can see, you are now root within an instance of Fedora. What exactly did we call there, though?

*   The `-i` flag starts an interactive container.
*   The `-t` flag creates a pseudo-terminal by attaching `stdin` and `stdout`.

If you want to name your container, you can use the `--name my-name` flag. For example, this spins up a container named *fedora-rocks*:

```bash
$ docker run -i -t --name fedora-rocks fedora /bin/bash
[root@a58980471b84 /]#
```

## List Containers

While your Fedora container is still running, open up another terminal. You can view your currently running containers with `docker ps`:

```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
6dc092fe3cc5        fedora              "/bin/bash"         11 seconds ago      Up 8 seconds                            my-fedora
```

You may be wondering, “Great, I can see my running containers! How about my stopped or old containers?” You can view those by using the `-a` flag:

```bash
$ docker ps -a
```

## Start and Stop Containers

Obviously, it is not useful to always have to keep a terminal open with your current container. You can start an already created container by passing its name to the `docker start` command:

```bash
$ docker start my-fedora
```

To run a command on a started container, use the `docker exec` command:

```bash
$ docker exec -i -t my-fedora /bin/bash
[root@6dc092fe3cc5 /]#
```

This launches an interactive terminal with our container just as when we used the  `docker run` command earlier. When we exit this terminal, however, the container will not stop like it did when we ran it earlier.

To stop the container, use the  `docker stop` command:

```bash
$ docker stop my-fedora
my-fedora
```

You can confirm that the container has stopped by listing the active containers:

```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

### Create an Application Container

Awesome! We've successfully ran a full blown Docker container with an accessible Unix shell. The Docker philosophy, however, is to try to keep each container to running one application. Let’s spin up a simple web server application. In the future we’ll write our own Docker image to host our own web application, but for this example we'll use a Python Flask server.

```bash
$ docker run -d -P training/webapp python app.py
```

This will spin up a container. We use the following two flags:
* The `-d` flag runs the container in the background.
* The `-P` flag tells Docker to map required network ports inside our container to our host.

Run the `docker ps -l` command to view details of the last container started.

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                     NAMES
7b97654081e1        training/webapp     "python app.py"     10 seconds ago      Up 9 seconds        0.0.0.0:32770->5000/tcp   admiring_goldwasser
```

By looking at the ports column, we can see that Docker has mapped the default Flask port (5000) to port 32770 on the host machine. We can now view our web application by going to http://localhost:32770. This is very useful as you can have applications running securely inside containers while still having access to what the application displays on your local machine. You can even specify certain ports when running the container. Stop the container by giving its name:

```bash
$ docker stop admiring_goldwasser
admiring_goldwasser
```

Imagine you had a server hosting Docker containers and wanted to have your Flask application on the default HTTP port:

```bash
$ docker run -d -p 80:5000 training/webapp python app.py
```

This time we use the `-p` flag rather than the `-P` flag and specify that we want to map port 80 of our local machine to port 5000 of our container. Run this on your workstation and then visit http://localhost/. You should be greeted with a “Hello world!”

Congrats! You have successfully run your first few Docker containers.
