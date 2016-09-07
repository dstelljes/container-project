# chroot

[chroot][man-chroot] is an old-timey Unix command that <b>ch</b>anges a process’s <b>root</b> directory. While it can't create a completely contained environment, there are quite a few things for which directory isolation can be handy:

*   **Installing software on an unbootable system:** When a system can’t be booted into, chroot can be used to run commands within its file system. The [Linux from Scratch][lfs-chroot] guides use chroot to install core software (including packages necessary to actually boot the system).

*   **Avoiding dependency hell:** If a piece of software requires a library that conflicts with the host system, installing and running it inside a chroot can avoid a collision.

*   **Limiting file access:** Some shared hosting services [use chroots to isolate user accounts][arch-sftp-chroot]. For instance, a tenant accessing the server via FTP might only be able to see the files for their website.

*   **Building and testing in a clean environment:** Building in a chroot guarantees that all dependencies are accounted for and that the external environment isn’t affecting the process. The [Arch developer wiki][arch-building-chroot] recommends that all packages be built within a clean chroot.

chroot is only a container environment in that it prevents the “jailed” process from accessing files or executing commands outside of the specified root. Because [everything in Unix is a file][everything-is-a-file], that’s a powerful restriction. However, there are several limitations that make chroot unsuitable for creating a completely isolated system:

*   A process with root privileges [can break out of the chroot][perl-breakout].

*   Programs might expect certain [FHS directories][fhs] (like `/tmp` and `/dev`) to be present.

*   chroot can't limit resource use (processor, memory, etc.).

In short, chroot is fine for isolating programs but isn’t meant to run isolated systems. We’ll see, though, that [LXC](../LXC/Introduction.md) and other container environments build on chroot to provide that functionality.

[arch-building-chroot]: https://wiki.archlinux.org/index.php/DeveloperWiki:Building_in_a_Clean_Chroot
[arch-sftp-chroot]: https://wiki.archlinux.org/index.php/SFTP_chroot
[everything-is-a-file]: https://en.wikipedia.org/wiki/Everything_is_a_file
[fhs]: https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard
[lfs-chroot]: http://www.linuxfromscratch.org/lfs/view/6.5/chapter06/chroot.html
[man-chroot]: http://linux.die.net/man/1/chroot
[perl-breakout]: http://pentestmonkey.net/blog/chroot-breakout-perl
