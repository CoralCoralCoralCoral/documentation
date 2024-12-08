# User Manual

## Note

The project includes an interactive map, this is provided by Mapbox which requires an API key in order to function, this is the only functionality that requires an API key, **with no key the rest of the app WILL continue to work as expected**.

If you are using the prebuilt docker images (**Recommended path**) during the first semester you do not need to do anything different as they will be built using a key in order for functionality to be tested and shown off.

**After semeter one** the prebuilt images may no longer have a working map, if you want this feature to be available again you will need to rebuild a portion of the app as detailed below.

**If you are locally building** you will need to provide a Mapbox API key for the map of the app to function.

To find out more about Mapbox [click here](https://www.mapbox.com/), for personal use the free tier allows plenty of requests, if you are an organisation check the licensing requirements for Mapbox as to whether a certain tier is needed.

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
