# User Manual

## Note

The project includes an interactive map, this is provided by Mapbox which requires an API key in order to function, this is the only functionality that requires an API key, **with no key the rest of the app WILL continue to work as expected**.

If you are using the prebuilt docker images (**Recommended path**) during the first semester you do not need to do anything different as they will be built using a key in order for functionality to be tested and shown off.

**After semeter one** the prebuilt images may no longer have a working map, if you want this feature to be available again you will need to rebuild a portion of the app as detailed below.

**If you are locally building** you will need to provide a Mapbox API key for the map of the app to function.

To find out more about Mapbox [click here](https://www.mapbox.com/), for personal use the free tier allows plenty of requests, if you are an organisation check the licensing requirements for Mapbox as to whether a certain tier is needed.

## Quick Start Guide

This is the simplest list of steps to run the app, if you need more information consult the full Installation Guide below.

1. Install [Docker Desktop](https://docs.docker.com/desktop/)
2. Open the Docker Desktop app (or otherwise start the docker services)
3. Download the 'docker-compose.yml' file in this folder
4. Open a terminal/console in the same folder as the compose file
5. Run the following command: `docker compose -f docker-compose.yml up -d`
6. Open your browser and visit 'http://localhost:8080/'

When you want to **stop** the app:

1. Open the Docker Desktop app
2. Go to the 'Containers' section
3. Press the stop button next to the top level container named 'Epidemic-Simulation'

*Alternatively...*

1. Open a terminal/console in the same folder as the compose file
2. Run the following command: `docker compose -f docker-compose.yml down`

## Installation Guide

### Using Docker Compose (Recommended)

The easiest way to run the app is using Docker, specifically using the Docker Compose file provided which starts and containerises all required services. For this the only thing you need to install on your device is Docker.

**Recommended Path**

Follow the installation guide [here](https://docs.docker.com/desktop/) to install the Docker Desktop app which provides the Docker Engine, Docker Desktop App, Docker Compose and more useful features

**Alternative Path**

Docker also provides a guide for installing just the Docker Engine [here](https://docs.docker.com/engine/install/) which may be useful for advanced users who do not need or want the additional Docker Desktop functionality, note that you may need to additionally install the Docker Compose plugin which will be needed to run the Compose file, instructions for that can be found [here](https://docs.docker.com/compose/install/)

**Post Docker install**

Once you have the Docker preqrequisite installed you can run the full stack by opening a command prompt (cmd/powershell on Windows, Terminal on MacOS/Linux) and run the following command

```bash
docker compose -f docker-compose.yml up -d
```

Open a browser and enter 'http://localhost:8080/', this will take you to the apps main page.

When you want to **stop** the app:

1. Open the Docker Desktop app
2. Go to the 'Containers' section
3. Press the stop button next to the top level container named 'Epidemic-Simulation'

*Alternatively*

1. Open a terminal/console in the same folder as the compose file
2. Run the following command: `docker compose -f docker-compose.yml down`

### Using Docker (not compose)

If you want to use docker but avoid using compose, maybe you have a distributed use case, you can build the app with docker but without compose.

Firstly you will of course need Docker installed, refer to the previous section for install assistance. Then you will want to install Git, more info [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

Open a terminal/console.

You will now want to clone the Sim-Server repository, enter the folder, and use Docker to build the image locally with the name 'sim-engine':
```bash
git clone https://github.com/CoralCoralCoralCoral/simulation-engine.git
cd simulation-engine
docker buildx build . -t sim-engine
```
Then leave the build folder:
```bash
cd ..
```
Next you can clone the Api-Server repository, enter the folder, and use Docker to build the image locally with the name 'api-server':
```bash
git clone https://github.com/CoralCoralCoralCoral/api-server.git
cd api-server
docker buildx build . -t api-server 
```

**Note: If you are using your own MapBox Api Key you will need to build the Docker image using the below instead**

Ensure the Api key is set as an environment variable, this only needs to be set for the build step, named 'mapbox_api_key'. On Windows using Powershell you can do `$mapbox_api_key=SECRET_KEY`, on MacOS and Linux you can use `mapbox_api_key=SECRET_KEY`.
```bash
docker buildx build . -t api-server --secret type=env,id=mapbox_api_key
```

See [Docker Buildx Secrets](https://docs.docker.com/reference/cli/docker/buildx/build/#secret) docs if you have any issues.

You can then run the Images indiviually, ensuring you start the RabbitMQ instance first.
```bash
docker run --detach --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:4.0-management 
```

Then the Api Server:
```bash
docker run --detach --rm --name api-server -p 8080:8080 -e SPRING_RABBITMQ_HOST=host.docker.internal api-server
```

Then the sim engine, ensuring to pass in the RabbitMQ connection details.
```bash
docker run --detach --rm --name sim-engine --env RMQ_URI=amqp://guest:guest@host.docker.internal:5672/ sim-engine
```

The easiest way to stop these running is the same as before, using the Docker Desktop app, and stopping the containers with the names set (rabbitmq, api-server, sim-engine).

Alternatively you can use:
```bash
docker kill rabbitmq api-server sim-engine
```

### Organisation Guide

As an organisation looking to serve the app to multiple users you can either follow the basic steps for a single user, installing the whole stack on a single device or have a more distributed setup based on your architecture.

If you decide to use the single user setup, be sure to edit the Docker Compose and network settings of your device to allow other clients on your network to access the container. The Spring instance serves on port 8080, this can be mapped to another port outside the container if needed/wanted.

Alternatively, it may be better to use a more distributed architecture, we would recommend running the Spring Api-Server and RabbitMQ instance on the same machine, with the Sim-Server instances running on their own machines, ensure the network setup allows the Sim-Servers to access the RabbitMQ instance. Running multiple Sim-Server instances on a single machine can help with availability, however ensure there is enough compute to drive all instances, the compute limit is the main reason to distribute the system.

The architecture used can change across organisations, using Docker (Swarm), Kubernetes, Cloud Compute or just building and running on multiple servers. The main requirement is that all Sim-Server instances can talk to RabbitMQ, and the Api-Server can talk to RabbitMQ, serve it's content and support websocket connections. By default RabbitMQ uses port 5672 and Spring uses port 8080.

You may also want to setup an on-prem DNS record to point to the Api-Server for ease of user access, along with generating and setting up SSL certs to allow for https and wss connections.

## User Guide

## Maintenance Guide

### Tech Stack

The tech stack consists of three main parts:

1. An Api Server
2. A [RabbitMQ](https://www.rabbitmq.com/) instance
3. A Simulation Service

There will be one Api server insance which serves up the static built UI/frontend, handles websocket connections to transmit simulation data and commands, and interacts with the RabbitMQ instance to pass messages to a simulation instance.

The [RabbitMQ](https://www.rabbitmq.com/) instance handles the messaging between the Api Server and any number of Simulation instances, message types include create-game, game-metrics, and game-commands.

Finally there is some number of simulation server instances, each simulation/game is contained by a single instance though one instance can run many simulations concurrently. The simulation server is responsible for doing the actual simulation work that is sent back to the client through Rabbit and the Api Server.

Running multiple copies of the simulation service can be beneficial, both for availability - if one instance on a host happens to crash there is still another running, and for distribution of load - having instances on multiple machines can ease the per machine compute workload.

### Api Server - [Repo Link](https://github.com/CoralCoralCoralCoral/api-server)
The Api Server is a Java Springboot application and follows generic Springboot standards and uses Gradle as a build tool. It's main function is to sit between a client and a Simulation engine instance, many Sim instances can be connected to many Clients via a single API Server instance. 

It can also be adapted to add further features such as using Spring's authorisation features to limit client's access and setup logins/user profiles for different individuals. The code gives a basic server without these extra features which can be applied as needed for different deployments.

The Configuration Classes in the Configuration Package (folder) control things like the auto-defined RabbitMQ Queues, Exchanges, Bindings etc, the CORS config for the app and the WebSocket/MessageBroker settings. In this case we use STOMP.

We have two Controller classes, again in an aptly named Package. The base Controller contains a simple root redirect to the static html of the UI, and a messaging endpoint to recieve the Game COmmand messages via STOMP. These commands are then forwarded over Rabbit. The other Controller Class contains the game creation endpoint, it creates a generic setup and attemps to serialise and send the appropriate data over Rabbit to a simulation engine instance and back as a response to the POST request to the client.

The Repository Package contains several Records used simply as skeletons for (de)serialising messages, either from Rabbit or from STOMP.

The final Package is Services, which contains a single service currently which is responsible for listening to a given RabbitMQ queue (game-metrics in this case) and do some processing, here it simply serialises the Metrics Map and forwards the data to the appropriate client using STOMP.

There are no static resources stored in the Api-Server repository, as all frontend development is done in the UI repo. This is then built and exported as a set of static resources which can be placed in the Api Server's static folder and built into the jar for serving to clients.
