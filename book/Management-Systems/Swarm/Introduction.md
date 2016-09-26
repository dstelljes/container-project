# Docker Swarm

Docker Swarm is the native clustering capabilities of Docker. This gives Docker the ability to pool multiple Docker hosts into one single entity and allows for scaling from one host to many. A lot of the popular user interfaces and other contain management systems utilize or can use Docker Swarm behind the scenes such as [Shipyard][shipyard] and [Rancher][rancher].

Docker Swarm can be deployed manually by downloading and installing the master swarm image onto a master node and downloading and installing the swarm agent onto client nodes. Swarms can also be created and added through the Docker CLI, which is technically the _swarm mode_ of Docker rather than the standalone Swarm product.

For now, we are omitting a guide on using Docker Swarm via the command-line and instead opting towards utilizing full container management systems for simplicities sake.

[shipyard]: https://shipyard-project.com/
[rancher]: http://rancher.com/
