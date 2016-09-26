# Container Management Systems

Container management systems are platforms for automating operations, deployments, and scaling of containers as well as managing clusters of computers running containers. Although overkill for a single node running a container environment, container management systems are very useful for lusters of nodes running many container environments. We're going to investigate some options for computer labs and using containers to manage lab processes.

There are many user interfaces and different types of container management systems. We're going to look into some of the most popular and ones that are purpose-specific to what we are looking to accomplish. We will be mainly looking into container management systems for Docker.

*   **[Docker Swarm][docker-swarm]:** Native clustering capabilities to turn a group of Docker engines into a single, virtual Docker engine. This allows for easy-to-scale applications.
*   **[Shipyard][shipyard]:** Built on top of Docker swarm, Shipyard adds a user interface to manage Docker images, containers, resources, and more within the swarm system.
*   **[Rancher][rancher]:** Brings an elegant user interface to managing a cluster and the containers and images running on the nodes of that cluster. Allows for easily monitoring system resources and distributing loads among multiple Docker engines.


[docker-swarm]: https://www.docker.com/products/docker-swarm
[shipyard]: https://shipyard-project.com/
[rancher]: http://rancher.com/
