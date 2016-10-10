# Container Distribution

Applications and systems being run through the use of containers can be distributed and scaled in two ways.

## Multi-container Distribution
The first way is to split the application among multiple containers running on a single host. For example, imagine we were running an application with a [Node.js][node] server connected to a [MongoDB][mongo] database. We can create one container that contains the Node.js server. We would then create a second container that contained the MongoDB database. These containers can then be linked together and communicate with each other.

This is beneficial as we are separating our containers and creating modularity. If the web server receives heavy load while the database does not, we can add more containers hosting the server rather than both the server and the database.

## Multi-host Distribution
The second way is to distribute an application among a container cluster. A container cluster is a system of hosts all capable of running one or multiple containers. This is helpful when one host does not have enough processing powers to handle the application. It is also beneficial as we can split our application among multiple machines. This means if one host crashes or goes down, only one part of our application will be down rather than the whole application.

[node]: https://nodejs.org/en/
[mongo]: https://www.mongodb.com/
