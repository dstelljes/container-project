# LXC

LXC (<b>L</b>inu<b>X</b> <b>C</b>ontainers) is a container environment designed to run isolated Linux systems on a shared kernel. Unlike [chroot](chroot.md), it creates a completely isolated environment with its own processor, memory, network interfaces, etc. Unlike [Docker containers](Docker/Introduction.md), which are designed to contain one application, LXC containers are intended to contain an entire system.

Under the hood, LXC [orchestrates a bunch of Linux kernel features][lxc-intro]:

*   **[capabilities][capabilities]:** Provides granular control over privileged processes.

*   **[cgroups][cgroups]:** Limits process resource usage.

*   **[chroot](../chroot/Introduction.md):** Isolates file system.

*   **[Namespaces][linux-namespaces]:** Isolate hostname, mount points, process/user/group IDs, and network stack.

*   **[seccomp][seccomp]:** Sandboxes applications.

*   **[SELinux][selinux]:** Enforces access control rules at the kernel level.

[capabilities]: http://man7.org/linux/man-pages/man7/capabilities.7.html
[cgroups]: https://en.wikipedia.org/wiki/Cgroups
[linux-namespaces]: https://en.wikipedia.org/wiki/Linux_namespaces
[lxc-intro]: https://linuxcontainers.org/lxc/introduction/
[seccomp]: https://en.wikipedia.org/wiki/Seccomp
[selinux]: https://en.wikipedia.org/wiki/Security-Enhanced_Linux
