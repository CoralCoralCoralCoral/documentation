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

When you want to stop the app:

1. Open the Docker Desktop app
2. Go to the 'Containers' section
3. Press the stop button next to the top level container named 'Epidemic-Simulation'

## Installation Guide

### Using Docker Compose (Recommended)

The easiest way to run the app is using Docker, specifically using the Docker Compose file provided which starts and containerises all required services. For this the only thing you need to install on your device is Docker.

**Recommended Path**

Follow the installation guide [here](https://docs.docker.com/desktop/) to install the Docker Desktop app which provides the Docker Engine, Docker Desktop App, Docker Compose and more useful features

**Alternative Path**

Docker also provides a guide for installing just the Docker Engine [here](https://docs.docker.com/engine/install/) which may be useful for advanced users who do not need or want the additional Docker Desktop functionality, note that you may need to additionally install the Docker Compose plugin which will be needed to run the Compose file, instructions for that can be found [here](https://docs.docker.com/compose/install/)

**Post Docker install**

Once you have the Docker preqrequisite installed you can run the full stack by opening a command prompt (cmd/powershell on Windows, Terminal on MacOS/Linux) and run the following command

```.bash
docker compose -f docker-compose.yml up -d
```

Open a browser and enter 'http://localhost:8080/', this will take you to the apps main page.

## User Guide

## Maintainance Guide

### Tech Stack

The tech stack consists of three main parts:

1. An Api Server
2. A [RabbitMQ](https://www.rabbitmq.com/) instance
3. A Simulation Service

There will be one Api server insance which serves up the static built UI/frontend, handles websocket connections to transmit simulation data and commands, and interacts with the RabbitMQ instance to pass messages to a simulation instance.

The [RabbitMQ](https://www.rabbitmq.com/) instance handles the messaging between the Api Server and any number of Simulation instances, message types include create-game, game-metrics, and game-commands.

Finally there is some number of simulation server instances, each simulation/game is contained by a single instance though one instance can run many simulations concurrently. The simulation server is responsible for doing the actual simulation work that is sent back to the client through Rabbit and the Api Server.

Running multiple copies of the simulation service can be beneficial, both for availability - if one instance on a host happens to crash there is still another running, and for distribution of load - having instances on multiple machines can ease the per machine compute workload.
