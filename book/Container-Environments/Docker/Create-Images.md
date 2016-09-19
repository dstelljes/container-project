# Creating Images

Obviously, sometimes you'll want to spin up a container with your own custom application. To accomplish this, we can create our own Docker image.

## Make a Dockerfile

To start, we need to make a Dockerfile. Docker uses this to build the image to the given specifications. We'll create a sample image that hosts this book on a Ubuntu OS. Create a directory and create a _Dockerfile_ inside of it:

```bash
$ mkdir containerbook
$ cd containerbook
$ touch Dockerfile
```

Using your favorite text editor, add the following:

```
# Base image of Ubuntu
FROM ubuntu:latest

# Install our required dependencies that Ubuntu doesn't include by default
RUN apt-get -y update && apt-get install -y nodejs && apt-get install -y npm && apt-get install -y git
RUN ln -s /usr/bin/nodejs /usr/bin/node

# Install gitbook
RUN npm install -g gitbook-cli

# Clone our project and install gitbook plugins specified within
RUN git clone https://github.com/dstelljes/container-project.git
RUN cd container-project/book && gitbook install

# Expose gitbook's port for Docker to see
EXPOSE 4000

# On start up of a container using this image, run these commands
# This will start a server with the latest version of our book
CMD cd container-project/book && git pull && gitbook serve
```

We can now build the image by running the following command:

```bash
$ docker build -t containerbook .
```

Once it builds, Docker will have an image titled _containerbook_. We can see this by running:

```bash
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
containerbook       latest              8e10e4e948f2        About a minute ago   727.8 MB
```

Finally, let's spin up a container with our newly created image:

```bash
$ docker run -d -p 9000:4000 --name container_book containerbook
```

This will throw up our gitbook container with our local port 9000 mapped to port 4000 in the container. Thus, we can now see this book by visiting http://localhost. To stop the container, run:

```bash
$ docker stop container_book
container_book
```

We have successfully created our first Docker image.
