# Software Containers

Prior to World War II, most international shipments were strapped to pallets or loaded in crates or bags. Cargo would be delivered to a warehouse near the dock and each piece would be individually loaded onto the ship. After the ship had reached its destination, each piece would be individually unloaded into another warehouse.

The break bulk system worked for most of the history of shipping, but it was far from optimal. Loading and unloading ships was a time-consuming process that required specialized equipment and involved hundreds of people. Cargo was often damaged and occasionally stolen, and ships had to be thoroughly cleaned between loads.

[Shipping containers][intermodal-containers] addressed those problems (and revolutionized the shipping industry) by antiquating the idea of individual pieces of cargo. Standardized containers eliminated the need for warehouses and large dock crews and introduced enormous improvements in efficiency, simplicity, and safety.

Software containers do for application deployment what shipping containers do for freight. Instead of relying on complicated scripts to prepare the deployment environment, software developers can pack configuration and dependencies into a container and be assured that the application will run correctly.

## Virtualization

To understand the benefits of containers, it helps to know a little bit about virtualization. Virtualization, as the name implies, refers to the use of virtual resources (memory, disk, etc.). Any reasonably designed system depends on virtualization. For instance, when a text editor writes to a file, it should be able to do so without any knowledge of the underlying storage device. Similarly, a web browser should be able to request a page without worrying about the underlying network interfaces or low-level protocols.

**Hardware virtualization** virtualizes a complete machine, allowing a complete operating system to run as a guest on top of the host operating system. The primary advantage of a virtual machine is that it separates a system from the hardware that it runs on, which is especially useful when running servers. If a virtual machine fails, the host can quickly restore a **snapshot** of the system (its settings and the state of any of its storage devices at a moment in time) or simply throw it out and start over from a clean images. If the host hardware fails or needs to be upgraded, its virtual machines can easily be transferred to another host.

Containers are an application of **operating system virtualization**. Containers act like virtual machines, but they share the host’s kernel. Sharing a kernel is more efficient (no overhead is incurred from booting and running another complete operating system), but less flexible (the guest operating system has to match the host). Containers are most frequently used to create isolated environments for applications and simplify the deployment process.

[intermodal-containers]: https://en.wikipedia.org/wiki/Intermodal_container
