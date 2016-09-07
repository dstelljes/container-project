# Container Environments

| Container environment      | File system isolation      | Processor and memory limits | Disk limits                  | Nesting                     | Root privilege isolation    |
|----------------------------|----------------------------|-----------------------------|------------------------------|-----------------------------|-----------------------------|
| [chroot][chroot]           | :confused:                 | :cry:                       | :cry:                        | :smile:                     | :cry:                       |
| [Docker][docker]           | :smile:                    | :smile:                     | :cry:                        | :smile:                     | :smile:                     |
| [LXC][lxc]                 | :smile:                    | :smile:                     | :confused:                   | :smile:                     | :smile:                     |

:smile:    Fully supported  
:confused: Partially supported  
:cry:      Not supported

*Adapted from [Wikipedia][environment-comparison].*

[chroot]: chroot/Introduction.md
[docker]: Docker/Introduction.md
[environment-comparison]: https://en.wikipedia.org/wiki/Operating-system-level_virtualization#Implementations
[lxc]: LXC/Introduction.md
