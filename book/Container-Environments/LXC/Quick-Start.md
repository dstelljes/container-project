# LXC Quick Start

## Install LXC

> **Note:** The installation process is easiest on Ubuntu. Other distributions can require a lot of configuration, and even older versions of Ubuntu are sometimes a pain. For best results, follow along with this quick start on a virtual machine with the latest version of Ubuntu Server. Alternatively, just skip ahead to [LXD][lxd-quick-start].

LXC can be found in the repositories for most Linux distributions. To check that it's installed and that nothing is missing or broken, run `lxc-checkconfig`:

    $ lxc-checkconfig
    Kernel configuration not found at /proc/config.gz; searching...
    Kernel configuration found at /boot/config-3.19.0-25-generic

    ...

## Create a container

To create a new container, use `lxc-create`:

    $ sudo lxc-create -t download -n first-container -- -d ubuntu -r xenial -a amd64

The `-t` flag tells LXC to download the container image [from linuxcontainers.org][lc-images] and the `-n` flag gives the container a name. The `-d`, `-r`, and `-a` flags are passed to the downloader and specify the type of root filesystem to download. So the above command will create a new container called *first-container* and based off of the downloaded Ubuntu 16.04 filesystem.

Once LXC has finished downloading the Ubuntu dependencies and setting up the container, `lxc-start` can be used to run commands within the container. Just for kicks, let’s do a stripped-down version of the `cowsay` example from the [Docker quick start][docker-quick-start]:

    $ sudo lxc-start -F -n first-container -- echo 'Hello world!'
    Hello world!

There are a few things going on here: The `-F` runs the container in the foreground, effectively taking over the console. Everything after the `--` will be run in the container. Like the Docker example, the container only runs for the duration of the command. Check the status of the container with `lxc-ls` and see that the container is stopped:

    $ sudo lxc-ls --fancy
    NAME            STATE   AUTOSTART GROUPS IPV4 IPV6
    first-container STOPPED 0         -      -    -    

## Attach to a container

You may be asking yourself why the previous section didn’t involve a talking cow. There’s a good reason: `cowsay` isn’t installed by default on most reasonable distributions and installing is less than straightforward. Try to use `lxc-start` and `apt-get` to install it:

    $ sudo lxc-start -F -n first-container -- apt-get -y install cowsay
    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done

    ...

    E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?

Those errors indicate that `apt-get` can’t download the needed files. Again, there’s a good reason: `lxc-start` is simply running a command inside the container. In order for networking (and other operating system things) to be present, the container actually has to boot its operating system.

Start the container again, but try some different options:

    $ sudo lxc-start -d -n first-container

The `-d` flag signals that the container should be run in the background (as a <strong>d</strong>aemon). `lxc-ls` should show that the container is running:

    $ sudo lxc-ls --fancy
    NAME            STATE   AUTOSTART GROUPS IPV4       IPV6
    first-container RUNNING 0         -      10.0.3.155 -    

Run `lxc-attach` to get into the container:

    $ sudo lxc-attach -n first-container
    root@first-container:/#


Notice that we now have a root shell inside the container. Let’s install `cowsay`:

    # apt-get -y install cowsay fortune
    ...
    # PATH=$PATH:/usr/games
    # fortune | cowsay
    ____________________________________
    / The last thing one knows in        \
    | constructing a work is what to put |
    | first.                             |
    |                                    |
    \ -- Blaise Pascal                   /
    ------------------------------------
          \   ^__^
           \  (oo)\_______
              (__)\       )\/\
                  ||----w |
                  ||     ||


[docker-quick-start]: ../Docker/Quick-Start.md
[lc-images]: https://images.linuxcontainers.org/
[lxd-quick-start]: ../LXD/Quick-Start.md
