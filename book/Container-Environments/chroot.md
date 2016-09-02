# chroot

[chroot][man-chroot] is an old-timey Unix command that **ch**anges a process's **root** directory. While it doesn't provide a completely isolated environment, this kind of separation is often useful:

*   **Install software on an unbootable system:** When a system can't be booted into, chroot can be used to run commands within its file system. The [Linux from Scratch][lfs-chroot] guides use chroot to install core software (including packages necessary to actually boot the system).

*   **Avoid dependency hell:** If a piece of software requires a library that conflicts with the host system, running it inside a chroot can avoid a collision.

*   **Limit file access:** Many shared hosting services use chroots to isolate user accounts. For instance, a tenant accessing the server via FTP might only be able to see the files for their website.

*   **Build and test in a clean environment:** Building in a chroot guarantees that all dependencies are accounted for and that the external environment isn't affecting the process. The [Arch developer wiki][arch-chroot] recommends that all packages be built within a clean chroot.

chroot is only a container environment in that it prevents the "jailed" process from accessing files or executing commands outside of the specified root. Among other limitations, a process with root privileges [can easily break out of the chroot][perl-breakout], most programs expect things like temporary directories and [device nodes][lfs-dev] to be present, and a chroot alone can't limit resource use (processor, memory, etc.).

For more complete isolation, an actual container environment has to be used.

[arch-chroot]: https://wiki.archlinux.org/index.php/DeveloperWiki:Building_in_a_Clean_Chroot
[lfs-chroot]: http://www.linuxfromscratch.org/lfs/view/6.5/chapter06/chroot.html
[lfs-dev]: http://www.linuxfromscratch.org/lfs/view/6.1/chapter06/devices.html
[man-chroot]: http://linux.die.net/man/1/chroot
[perl-breakout]: http://pentestmonkey.net/blog/chroot-breakout-perl
