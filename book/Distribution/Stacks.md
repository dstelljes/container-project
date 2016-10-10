# Application Stacks

Although there does not seem to be a formal name for modular, multi-container applications, we will use the term _stacks_ as a shorthand for such systems. The idea is that you can split your application into a stack of containers (similar to the full-stack design of a web service) which can easily be deployed together.

These stacks or groups of containers (which can be on a single host or part of a cluster of hosts) allow for separation and isolation of each part of an application. This makes it easier to scale certain parts of applications as well as fixing certain parts of applications without modifying the whole application.

## Voting Application Stack Example

To give an example of a multi-container stack setup, let's take a look at a small application we created. We have a voting application that allows you to vote for whichever color is better: red or blue. It is a Node.js (Express) server that stores the data in a Redis database. This is a perfect scenario to build a container stack and have one container for the application and another for the database.

Let's start by taking a look at the application. The source code can be viewed on [GitHub][example]. You will want to clone the repository and switch to the `example` branch to follow through with the tutorial. Otherwise, the master branch has all Docker stuff ready to go.

All of the sources files for the project are located in the `src/` directory. To start the application, you would run `npm start`. Let's start by creating a Dockerfile for this application:

```
FROM node:argon

# Create our application directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app


# Copy our files and install node dependencies
COPY package.json /usr/src/app
RUN npm install
COPY . /usr/src/app

# Open our port and run the server
EXPOSE 3000
CMD ["npm", "start"]
```

We build our image based on node image from Docker Hub. We copy our source files over and finally run our application. To build the image, run:

```bash
$ docker build -t voting-app .
```

We can now spin up a container and see what happens:

```bash
$ docker run -it -p 61000:3000 --name voting-app voting-app
```

Right away, we see that we are getting errors saying the application cannot connect to a Redis server:

```bash
Voting application listening on port 3000!
Redis error: Error: Redis connection to 127.0.0.1:6379 failed - connect ECONNREFUSED 127.0.0.1:6379
```

Let's create a Redis container and link it to our container.

```bash
$ docker run --name voting-app-2 --link redis1
```

Let's spin up our application again, this time linking our containers:

```bash
$ docker run -it -p 61000:3000 --link redis1:redis voting-app
```

We get no errors this time. If we visit [http://localhost:61000](http://localhost:61000), we can now see everything is working properly. This, however, would be very hard to setup if we had more than two things in our stack. The proper way to do this is to use Docker compose.

### Docker Compose

Let's utilize Docker compose to do this so we can do this all in one step. We start by making a `docker-compose.yml` file:

```
version: '2'
services:
 voting-app:
   build: .
   ports:
    - "61000:3000"
   depends_on:
    - redis
 redis:
   image: redis
```

This file is doing a few things for us:
* Using version 2 of Docker compose
* Creates two services: the _voting-app_ service and the _redis_ service
* Builds the voting-app image from the Dockerfile in the current directory
* Forwards port 3000 on the container to 61000 on the host machine
* Links the voting_app service to the redis service

Make sure your containers from the previous section are stopped and then run the following command:

```bash
$ docker-compose up
```

A lot of things will happen, and then your stack is running! Visit [http://localhost:61000](http://localhost:61000) to confirm. You can run it with the `-d` flag to run it in the background.

Docker compose makes it very simple to link services together and create a container stack. 



[example]: https://github.com/devshawn/docker-compose-example
