# Testing within containers

Testing is an essential part of the development process. Unit tests and functional (end-to-end) tests should be run on every build. If you're developing within a container, tests should be able to be run as its own container as well.

To run any of the examples given below, you will want to clone our [running-tests-in-docker][repo] repository.

## Unit Tests

Unit tests are essential in any application. We created a small example in the `unit` directory of our `running-tests-in-docker` repository. It runs Karma + Jasmine tests doing basic unit tests on some javascript functions.

Make sure you have cloned our repository. We have the following `Dockerfile.unit`:

```
FROM node:argon

MAINTAINER Shawn Seymour <seymo079@morris.umn.edu>
MAINTAINER Dan Stelljes <stell124@morris.umn.edu>

# Create our application directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app


# Copy our files and install node dependencies
COPY package.json /usr/src/app
RUN npm install
COPY unit/. /usr/src/app/unit

# Run our tests
CMD ["npm", "run", "unit"]
```

This Dockerfile creates our application directory, copies the unit test example, installs node dependencies, and will run the unit tests when a container is launched.

To build the Dockerfile, open up a terminal in the root directory of our repository.

```bash
$ docker build -t unit-test-example -f Dockerfile.unit .
```

We use the `-f` flag to specify a Dockerfile as we are not using the default name for a Dockerfile. Once the image finishes running, we can run the following:

```bash
$ docker run -t unit-test-example
```

This will spin up a container and output the karma unit test results. The `-t` run flag is to attach a pseudo-terminal so we can see the output.

Now, if you updated your application code you would have to rebuild the image and run a new container. We'll show later how to have an image that will have the latest code every time you create a container.
