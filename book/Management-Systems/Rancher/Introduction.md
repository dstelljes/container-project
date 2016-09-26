# Rancher

Rancher is an open-source container management system for operating Docker at scale. It can be installed as a standalone application within a system. Rancher Labs, however, has also built an operating system for running Docker containers that includes Rancher by default (conveniently titled RancherOS). We are more concerned with the Rancher application rather than the whole operating system.

Rancher hosts an elegant web interface to manage a cluster of Docker nodes. It allows for building multi-container stacks, implementing load balances for applications to distribute loads over currently-available Docker nodes, and allow to easily download, update, and install images over the whole cluster. It provides easy-to-read graphs for monitoring both system-wide and per-container resource usages. Of course, it makes it trivial to spin up a container on any node in the cluster.

## Hosts

Rancher provides a list of all of the nodes within the current environment's cluster. An environment is a defined cluster, such as a computer lab. The hosts page displays information such as the IP address, current Docker version, memory, available disk space, and much more.

![alt text][hosts]

We can also view the details of a single host. This shows detailed information regarding the host's underlying system and current resource usages. This is great for managing a cluster of workstations and allows for system-wide monitoring of a node that could be running many containers.

![alt text][host-details]

Within the host details page, it lists the containers that are present on the host whether they are currently running or not.

![alt text][host-list]

## Containers

Rancher has a listing of every container on any host within the cluster. This can be useful for a mass-overview of the cluster and what it is being used for as well as the distribution of containers of the cluster.

![alt text][container-list]

Rancher includes details on single-containers running on a host. For example, here is a look at a container of our containerbook image running:

![alt text][book1]

This gives us a great look into how much of our system resources are being used by a single container. It also will give you the IP address of the container, the open ports on the container, and much more. Of course, we are provided with the ability to spin up containers. There are a lot of cool features including scheduling containers over multiple hosts, networking between containers, assigning shared volumes, and more.

![alt text][add-container]

Rancher gives us a lot of visualization tools and has a lot of more in-depth features than shown above. It is definitely a full-fledged container management system and seems to be farther along and nicer than Shipyard.

[hosts]: hosts.png "Hosts"
[host-details]: host-details.png "Details of a single host"
[host-list]: host-list.png "List of containers on a single host"
[container-list]: container-list.png "List of containers on any host"
[book1]: book1.png "Single container details"
[add-container]: add-container.png "Adding a container"
