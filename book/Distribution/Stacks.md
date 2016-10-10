# Application Stacks

Although there does not seem to be a formal name for modular, multi-container applications, we will use the term _stacks_ as a shorthand for such systems. The idea is that you can split your application into a stack of containers (similar to the full-stack design of a web service) which can easily be deployed together.

These stacks or groups of containers (which can be on a single host or part of a cluster of hosts) allow for separation and isolation of each part of an application. This makes it easier to scale certain parts of applications as well as fixing certain parts of applications without modifying the whole application.
