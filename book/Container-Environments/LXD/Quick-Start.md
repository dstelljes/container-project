# LXD Quick Start

## Install LXD

> **Note:** Like LXC, working with LXD is easiest on Ubuntu. If you’re on another distribution, you’ll probably have to compile from source. Whether it gains traction elsewhere is yet to be seen; as of this writing, the project is still less than two years old and its first production-ready release was less than half a year ago.

> **Cool thing, though:** You can try LXD online at https://linuxcontainers.org/lxd/try-it/. There’s also a step-by-step introduction to some interesting features.

Installing LXD on recent versions of Ubuntu is as simple as running `apt`:

    $ sudo apt install lxd

One interesting feature of LXD is that [it’s designed to take advantage of advanced features of a number of storage backends][lxd-backends]. The directory storage backend (what LXC and Docker use by default) doesn’t require any configuration, but the LXD team recommends ZFS. Though optional, it’s also really easy to install:

    $ sudo apt install zfsutils-linux

After LXD has been installed, configure it with `lxd init`:

    $ sudo lxd init
    Name of the storage backend to use (dir or zfs) [default=zfs]:
    Create a new ZFS pool (yes/no) [default=yes]?
    Name of the new ZFS pool [default=lxd]:
    Would you like to use an existing block device (yes/no) [default=no]?
    Size in GB of the new loop device (1GB minimum) [default=10GB]:
    Would you like LXD to be available over the network (yes/no) [default=no]?
    Do you want to configure the LXD bridge (yes/no) [default=yes]?
    Warning: Stopping lxd.service, but it can still be activated by:
      lxd.socket
    LXD has been successfully configured.

It’s worth reading through the configuration options, but the defaults probably don’t need to be changed.

## Create a container

From this point forward, use the `lxc` command to interact with LXD. On its face, this is sort of confusing, but it reflects that LXD is just a management system around LXC containers.

Start by launching a new container:

    $ lxc launch images:fedora/24 another-cow-example
    Creating another-cow-example
    Retrieving image: 100%
    Starting another-cow-example


To unpack that: `launch` creates a container and starts it. `images:fedora/24` uses the Fedora 24 image from the `images:` repository. `another-cow-example` is the new container’s name. If all goes well, `lxc list` should show the new container:

    $ lxc list
    +---------------------+---------+----------------------+------+------------+-----------+
    |        NAME         |  STATE  |         IPV4         | IPV6 |    TYPE    | SNAPSHOTS |
    +---------------------+---------+----------------------+------+------------+-----------+
    | another-cow-example | RUNNING | 10.80.148.159 (eth0) |      | PERSISTENT | 0         |
    +---------------------+---------+----------------------+------+------------+-----------+

Use `lxc exec` to run commands in a container. One perk of LXD is that container networking is configured by default, so `cowsay` can be had in two commands without dropping into a shell:

    $ lxc exec another-cow-example -- dnf -y install fortune-mod cowsay
    ...
    $ lxc exec another-cow-example -- bash -c 'fortune | cowsay'
    ________________________________________
    / If you waste your time cooking, you'll \
    \ miss the next meal.                    /
    ----------------------------------------
    \   ^__^
     \  (oo)\_______
        (__)\       )\/\
            ||----w |
            ||     ||


Use `lxc stop` to stop the container:

    $ lxc stop another-cow-example

And to destroy the container completely, use `lxc delete`:

    $ lxc delete another-cow-example

## Take some snapshots

One of LXD’s main selling points is its snapshot creation. Create another image (this time using Ubuntu):

    $ lxc launch ubuntu: quick-start

Start by taking a snapshot of the container in its pristine state:

    $ lxc snapshot quick-start clean

(Here, `clean` is the name of the snapshot.) `lxc info` will show a list of snapshots along with some other machine info:

    Name: quick-start
    Architecture: x86_64
    ...
    Snapshots:
      clean (taken at 2016/09/26 05:05 UTC) (stateless)

`lxc file` manipulates files in the container. `lxc file push`, for instance, moves a file from the host into the container:

    $ echo 'this is super important' > /tmp/super_secret.txt
    $ lxc file push /tmp/super_secret.txt quick-start/usr/super_secret.txt

Taking another snapshot here...

    $ lxc snapshot quick-start secret-file

... might be helpful later if something bad happens to the container:

    $ lxc exec quick-start -- bash -c 'rm -rf /usr'

To restore a previous snapshot, use `lxc restore`:

    $ lxc restore quick-start secret-file

And verify that it worked:

    $ lxc file pull quick-start/usr/super_secret.txt super_secret_restored.txt
    $ cat super_secret_restored.txt
    this is super important

## Set some limits

LXD makes setting resource limits easy. For instance, to throttle network I/O across all containers, try the following:

    $ lxc profile device set default eth0 limits.ingress 100Mbit
    $ lxc exec quick-start -- wget http://speedtest.atlanta.linode.com/100MB-atlanta.bin -O /dev/null

[lxd-backends]: https://github.com/lxc/lxd/blob/master/doc/storage-backends.md
