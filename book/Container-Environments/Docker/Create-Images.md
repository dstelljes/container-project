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
FROM ubuntu:latest
RUN apt-get -y update && apt-get install -y nodejs && apt-get install -y npm && apt-get install -y git
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN npm install -g gitbook-cli
RUN git clone https://github.com/dstelljes/container-project.git
RUN cd container-project/book && gitbook install
EXPOSE 4000

CMD cd container-project/book && git pull && gitbook serve
```

We can now build the image by running the following command:

```bash
$ docker build -t containerbook .
```
