# Useful Docker Commands

There are a lot of useful Docker commands, but here is a short, easy-to-read list of commonly used and useful commands.

## Listing Containers

Command | Description
-------------- | ---
`docker ps`    | Lists details of all of the currently running containers
`docker ps -a` | Lists details of all containers on the machine
`docker ps -l` | Lists details of the last created container

## Running Containers

Command | Description
------------------------------ | ---
`docker start [name]`          | Starts an already-created container with given [name]
`docker run [image] [command]` | Runs a container with the given [image] and then runs the given [command]
`docker stop [name]`           | Stops a currently-running container with given [name]
`docker kill [name]`           | Kills a currently-running container with given [name] (use if it will not stop for some reason)

## Using Docker Images

Command | Description
----------------------------- | ---
`docker images`               | Lists the images on a local workstation
`docker search [name]`        | Searches for an image on Docker Hub
`docker pull [name]`          | Downloads an image from Docker Hub onto a workstation
`docker search [name]`        | Searches for an image on Docker Hub
