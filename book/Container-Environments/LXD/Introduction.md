# LXD

LXD is an easier way to run [LXC][lxc] containers. It provides a simple interface around LXC’s low-level tools and, like Docker, it uses a long-running daemon to facilitate resource limiting and migration. It’s also designed with security in mind, aiming to significantly reduce the amount of configuration needed to create unprivileged containers.

All LXD containers are based on **images**, which are analogous to LXC’s **templates**. Container images can be published and subsequently used by other LXD hosts. The LXD daemon watches remote images and downloads updates as they become available.

LXD offers some other improvements over LXC, most notably **profiles**. Profiles are configurations that can be applied to multiple containers. If a container is built with multiple profiles, the profiles will be applied in the order that they were defined.

[lxc]: ../LXC/Introduction.md
