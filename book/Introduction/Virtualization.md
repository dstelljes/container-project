# Virtualization

To understand the benefits of containers, it helps to know a little bit about virtualization. Virtualization, as the name implies, refers to the use of virtual resources (memory, disk, etc.). Most reasonably designed systems depend heavily on virtualization. For instance, when a text editor writes to a file, it does so without having to worry about whether the file is on a hard drive, a flash drive, an encrypted volume, the network, or whatever. Similarly, a web browser requests content without dealing with low-level network protocols or the system’s network interfaces.

Virtualization is as much about security as it is about abstraction. By virtualizing resources, a system can impose restrictions: what actions can be performed, what properties are visible, and how much can be used.

## Hardware virtualization

**Hardware virtualization** virtualizes a complete machine, allowing a complete operating system to run as a guest on top of the host operating system. The primary advantage of a virtual machine is that it separates a system from the hardware that it runs on, which is especially useful when running servers. If a virtual machine fails, the host can quickly restore a **snapshot** of the system (its settings and the state of any of its storage devices at a moment in time) or simply throw it out and start over from a clean image. If the host hardware fails or needs to be upgraded, its virtual machines can easily be transferred to another host.

Virtual machines are also used to run different operating systems on the same computer. Software like [Parallels][parallels] and [VMware Fusion][fusion] run Windows on top of macOS, and more general applications like [VirtualBox][virtualbox] run a variety of guest operating systems on Linux, macOS, and Windows guests. [Game console emulators][console-emulators] rely on hardware virtualization to run classic games (legally or otherwise) on new hardware.

## Operating system virtualization

Containers are an application of **operating system virtualization**. Containers act like virtual machines, but they share the host’s kernel. Sharing a kernel is more efficient (no overhead is incurred from booting and running another complete operating system), but less flexible (the guest operating system has to match the host). Containers are most frequently used to create isolated environments for applications and simplify the deployment process.

[console-emulators]: https://en.wikipedia.org/wiki/List_of_video_game_emulators
[fusion]: http://www.vmware.com/products/fusion.html
[parallels]: http://www.parallels.com/
[virtualbox]: https://www.virtualbox.org/
