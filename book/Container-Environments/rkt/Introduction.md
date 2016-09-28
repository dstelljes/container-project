# rkt

rkt (pronounced “rocket”) is a fairly new container runtime developed by the [CoreOS][coreos] team. rkt aspires to the following goals:

*   **Secure by default:** Unlike the Docker daemon, rkt can run as an unprivileged process. It also supports running containers in hardware-isolated virtual machines (i.e., instead of sharing the host kernel with Linux cgroups and namespaces, rkt can run containers in a completely isolated hypervisor).

*   **Composable:** rkt containers are described in terms of init systems (`upstart` on Ubuntu and `systemd` elsewhere) and are designed to work with a variety of management software.

*   **Standardized**: rkt promotes the [App Container specification][appc] as a way to define, run, and discover containers. rkt can also run Docker images.

rkt is primarily a reaction to what CoreOS calls Docker’s [broken security model][rkt-announcement] (namely, that all containers run on a Docker daemon with root privileges). Also, there are some key philosophical differences: rkt takes a Unix-like, “do one thing well” approach while Docker is more monolithic.

[appc]: https://github.com/appc/spec/
[coreos]: https://coreos.com/
[rkt-announcement]: https://coreos.com/blog/rocket/
