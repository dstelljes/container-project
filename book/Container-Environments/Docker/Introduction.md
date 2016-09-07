# Docker

## What is it?
Docker is a platform for developing, shipping, and deploying applications. It is meant to run applications isolated in their own *containers*.

Docker containers are a lightweight solution to running applications. Instead of virtualizing hardware like virtual machines do, containers rest on top of the host's operating system and share as many resources as possible.

The Docker daemon creates and manages Docker objects. These objects can be containers, images, networks, and more.

## Docker Resources
* **Images**: These are read-only templates. An example of this would be a Fedora operating system running a Node.js application. These images are used to create containers and are meant to be shared.

* **Containers**: These hold everything that is needed for an application to run. They are created from images. They can be run, started, stopped, moved, and deleted. They are isolated from each other and secure.

* **Registries**: These are public or private repositories holding Docker images. They are for distributing images to the public or to others within your own network.
