# Container Environments

The need for isolated environments has been around for a long time, but software containers recently gained popularity as a way to easily move applications from development into production without using full-fledged virtual machines. ([Vagrant][vagrant], a popular development tool, uses virtual machines to create local versions of production environments.) This chapter outlines a few available container environments and attempts to show the differences between them:

| Container environment      | File system isolation      | Processor and memory limits | Disk limits                  | Nesting                     | Root privilege isolation    |
|----------------------------|----------------------------|-----------------------------|------------------------------|-----------------------------|-----------------------------|
| [chroot][chroot]           | :confused:                 | :cry:                       | :cry:                        | :smile:                     | :cry:                       |
| [Docker][docker]           | :smile:                    | :smile:                     | :cry:                        | :smile:                     | :smile:                     |
| [LXC][lxc]                 | :smile:                    | :smile:                     | :confused:                   | :smile:                     | :smile:                     |

:smile:    Fully supported  
:confused: Partially supported  
:cry:      Not supported

*Adapted from [Wikipedia][environment-comparison].*

## Operating System Containers vs. Application Containers

Containers are primarily used for two purposes, user space isolation and application packaging. Operating system containers provide the former—in most cases, they function like complete virtual machines. Application containers provide the latter—they're responsible for one service and its immediate dependencies.

LXC and other technologies like OpenVZ and Solaris Containers are primarily used to create operating system containers. Like virtual machines, operating system containers are generally created from images that determine the initial state of the container (contents, settings, etc.).

Docker is designed to create application containers, and the underlying architecture is a little different. Rather than creating a container from a single image, Docker containers are layered. Each layer describes itself in terms of differences between it and its parent container. A container for a continuous integration server might be composed of the following layers:

1.  **Base image**: Ubuntu Server
2.  **JavaScript toolchain**: Node.js
3.  **Python toolchain**: Python
4.  **Continuous integration service**: Jenkins, Java, Tomcat
5.  **Writeable layer**: temporary files, build artifacts

This is interesting for a couple of reasons. First, layering encourages reuse of common components and reduces duplication. Layers can be independently versioned, making it easy to roll back changes and see differences. As a convenient side effect, containers can be transferred solely by sending changes (similar to Git). Second, the application container isn’t responsible for things like a database server—another container handles that.

## Privileged Containers

Not all containers are created equal. In some cases, it’s desirable to run a container with elevated privileges; most of the time, it’s safer to limit what the container can do. Unfortunately, the terminology varies among different container environments.

In LXC, an unprivileged container maps internal [uids and gids][uid] to an unused range on the host system. For instance, a process running as uid 0 (root) in the container might actually be running as process 42000 on the host. If, somehow, something in the container escaped and gained access to the host system, it would run as uid 42000 and would have no elevated privileges. A privileged container, by contrast, is isolated, but its processes run as root on the host system. One pitfall of the LXC privilege system is that [it’s significantly harder to create unprivileged containers than privileged ones][lxc-getting-started].

Docker’s privileged containers give the container carte blanche access to devices and kernel features. The introduction of privileged containers brought with it the ability to [run Docker within itself][docker-in-docker], for people who are into that kind of thing.

It’s worth noting that the Docker daemon, regardless of whether it’s hosting privileged containers or not, runs containers as root. This understandably made people uncomfortable, as any user able to interact with Docker [effectively has root privileges][docker-root]. As of [Docker 1.10][docker-1.10], privileges for the Docker daemon and individual containers can be handled separately, though the daemon itself still requires root privileges.

[chroot]: chroot/Introduction.md
[docker]: Docker/Introduction.md
[docker-1.10]: https://blog.docker.com/2016/02/docker-1-10/
[docker-in-docker]: https://blog.docker.com/2013/09/docker-can-now-run-within-docker/
[docker-root]: http://reventlov.com/advisories/using-the-docker-command-to-root-the-host
[environment-comparison]: https://en.wikipedia.org/wiki/Operating-system-level_virtualization#Implementations
[lxc]: LXC/Introduction.md
[lxc-getting-started]: https://linuxcontainers.org/lxc/getting-started/
[uid]: https://en.wikipedia.org/wiki/User_identifier
[vagrant]: https://www.vagrantup.com/
