# Shipyard

Shipyard is a container management system for Docker which is build on top of Docker Swarm. It is really nice due to the fact that it is a tool for managing a cluster of nodes or a computer lab and monitoring all containers and images being utilized on these nodes. This is usable for a computer lab as it is possible to see which containers are hogging up resources of the parent nodes as well as giving the ability to easily run commands on the containers, delete the containers, install new images onto all of the machines, and more. And, it provides a beautiful web interface to do this all from rather than hacking away at a terminal for hours.

## Containers

Shipyard allows interacting with containers on any of the nodes within the cluster. A shipyard admin can spin up a container on any node in the cluster and then view its logs, resource usages, run commands within the cluster, and more. Shipyard's main page is a listing of the containers being hosted within the cluster, as shown below.

![alt text][containers]

Shipyard has a clean interface for spinning up containers. It is much easier to specify a lot of requirements using the web interface here rather than through Docker's command-line interface.

![alt text][deploy]

You can also pause, stop, restart, delete, and do much more with each container within the web interface.

![alt text][details]

As you can see, shipyard makes it a lot easier to manage containers especially if you had a whole computer lab running Docker.

[containers]: containers.png "List of containers"
[deploy]: deploy.png "Deploying a new container"
[details]: details.png "Detailing a container"
