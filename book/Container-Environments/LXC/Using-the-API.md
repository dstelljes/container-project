# Using the LXC API

LXC ships with C and Python bindings that can be used to manipulate containers programmatically. It's arguably easier to do the Quick Start in Python than on the command line:

```python
import lxc
import sys

# The API documentation is mostly nonexistent, but figuring out what's available
# is relatively straightforward:
#   https://github.com/lxc/lxc/blob/master/src/python-lxc/lxc/__init__.py
#
# Also, some examples can be found here:
#   https://linuxcontainers.org/lxc/documentation/

# Most interaction with LXC will happen through the Container object:
container = lxc.Container("fortune-telling-cow")

# If the container doesn't exist, we can create it in a manner not dissimilar to
# the command line:
if not container.defined:
  success = container.create("download", lxc.LXC_CREATE_QUIET, {
    "dist": "ubuntu", "release": "xenial", "arch": "amd64"
  })

  if not success:
    print("Couldn't create the container 🐮", file = sys.stderr)
    sys.exit(1)

# The Python bindings are a pretty thin wrapper around the C bindings, so we
# wind up checking booleans rather than catching exceptions:
if not container.start():
  print("Couldn't start the container 🚀", file = sys.stderr)
  sys.exit(1)

# The timeout argument is apparently the preferred way to wait for the container
# to establish network connectivity:
if not container.get_ips(timeout = 30):
  print("The container couldn't get online 🌎", file = sys.stderr)
  sys.exit(1)


# As before, we'll attach to the container and install cowsay and fortune. We'll
# get an exit code back (useful for checking whether a command actually worked):
update = container.attach_wait(lxc.attach_run_command, ["bash", "-c", "apt-get -y update > /dev/null"])
install = container.attach_wait(lxc.attach_run_command, ["bash", "-c", "apt-get -y install cowsay fortune > /dev/null"])

if update is not 0 or install is not 0:
  print("Couldn't install packages 📦", file = sys.stderr)
  sys.exit(1)

# Let's get a fortune:
fortune = container.attach_wait(lxc.attach_run_command, ["bash", "-c", "/usr/games/fortune | /usr/games/cowsay"])

# Finally, shut down the machine:
if not container.shutdown(10):
  container.stop()
```
