# Product Document

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

_Alternatively..._

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

_Alternatively_

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

Then leave the build folder, clone the Api-Server repository, and enter the folder,:

```bash
cd ..
git clone https://github.com/CoralCoralCoralCoral/api-server.git
cd api-server
```

Ensure the MapBox Api key is set as an environment variable, this only needs to be set for the build step, named 'mapbox_api_key'. On Windows using Powershell you can do `$mapbox_api_key=SECRET_KEY`, on MacOS and Linux you can use `mapbox_api_key=SECRET_KEY`

Then use Docker to build the image locally with the name 'api-server'.:

```bash
docker buildx build . -t api-server --secret type=env,id=mapbox_api_key
```

**Note: If you do not have a MapBox API key you can use the below instead, no default key is provided**

```bash
docker buildx build . -t api-server
```

See [Docker Buildx Secrets](https://docs.docker.com/reference/cli/docker/buildx/build/#secret) docs if you have any issues.

You can then run the Images indiviually, ensuring you start the RabbitMQ instance first, wait 30 seconds - 1 minute for the Rabbit image to fuly start up, the other parts of the app require Rabbit is functional to successfully start. If you are not sure, open Docker Desktop and click on the RabbitMQ container, if the logs are still moving then wait for them to stop.

```bash
docker run --detach --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:4.0-management
```

Then the Api Server:

```bash
docker run --detach --rm --name api-server -p 8080:8080 --env SPRING_RABBITMQ_HOST=host.docker.internal api-server
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

### Building from source

This section may be for you if you can't or don't want to use Docker, if you simply prefer building from source or if you want to build as you develop the application.
If you are not comfortable using a terminal/console it may not be the path for you, however anyone should be able to follow these steps with some level of terminal experience.

Open a terminal and create a folder to store application files. You should start each of the below sections from the folder you create, you may choose another name or location if you wish.

```bash
mkdir Coral-Epidemic-Sim
cd Coral-Epidemic-Sim
```

#### <ins>UI<ins/>

**Requirements**

-   Node: Install instructions can be found [here](https://nodejs.org/en/download/package-manager), 23.1 was used during development
-   NPM: Assuming you follow the standard path for installing Node NPM will also be installed, 10.9 was used during development
-   MapBox API Key: If you have a mapbox api key you should ensure it is set as an environment variable for the build step, it is not required during runtime

**Build steps**

The first step is to clone the remote repository and enter the cloned folder.

```bash
git clone https://github.com/CoralCoralCoralCoral/ui.git
cd ui
```

Then install npm dependencies.

```bash
npm install
```

Finally build the UI project into a set of static files.

```bash
npm run build
```

After some time you will have the static files built in a folder called 'out', these are what you will need later.

#### <ins>Api Server<ins/>

**Requirements**

-   UI static files: if you haven't already follow the previous set of instructions to build the UI
-   Java Development Kit(JDK): you can get away with just a Java Runtime Environment to run the app, but will need the extra development tools of the JDK to build it, Java 17 was used during development, downloads can be found [here](https://adoptium.net/en-GB/temurin/releases/?version=17)
-   Gradle preqrequisites: You do not need gradle installed but you do need to meet the preqrequisites setout [here](https://docs.gradle.org/current/userguide/installation.html#sec:prerequisites)

**Build steps**

The first step is to clone the remote repository and enter the cloned folder.

```bash
git clone https://github.com/CoralCoralCoralCoral/api-server.git
cd api-server
```

Next copy the built static files from the UI into the static folder of the api-server which can be found in `src/main/resources/static/`. Assuming you follow the recommended folder structure you can use the below commands, otherwie you may need to change them slightly, alternatively you can use a graphical file explorer to copy the files.

```bash
cp -r ../ui/out/* ./src/main/resources/static/
```

Finally you can build a 'boot jar', sometimes called a 'fat-jar' which bundles all dependencies and data into a single file (archive) which can be ran later.

```bash
./gradlew clean bootJar
```

The built jar will be placed in `build/libs/` with a name similar to `EpidemicSimApiServer-0.0.1-SNAPSHOT.jar`, if you wish this can be moved somewhere else or left where it is, just be sure to remember where you put it as you will need to reference it to run the app.

**Running the Api Server**

Running the Api Server is simple as long as you remember where you leave the jar, from the same folder as the jar you can run the following, be sure you match the name if it is different to the below example (using tab can autocomplete the name for you)

```bash
java -jar EpidemicSimApiServer-0.0.1-SNAPSHOT.jar
```

**Note:** Attempting to run the Api Server without RabbitMQ running will give errors as it cannot communicate and create the messaging constructs needed

#### <ins>Sim Engine<ins/>

**Requirements**

-   Golang: installation guide can be found [here](https://go.dev/doc/install), golang version 1.23 was used during development

**Build steps**

The first step is to clone the remote repository and enter the cloned folder.

```bash
git clone https://github.com/CoralCoralCoralCoral/simulation-engine.git
cd simulation-engine
```

Next download the dependencies.

```bash
go mod download
```

Then build the sim-engine.

```bash
go build -o sim-engine main.go
```

This will build an exeutable for the current platform with the filename sim-engine in the current folder, you can move it like the Api Server jar, just be sure to remember where you put it. If you want to build for another platform there is a good guide [here](https://www.digitalocean.com/community/tutorials/how-to-build-go-executables-for-multiple-platforms-on-ubuntu-16-04#step-4-building-executables-for-different-architectures).

If you want to optimise your build (size wise at least) you can use the following to strip symbol and debug information, though this is **not recommended** unless you know what you are doing, debug symbols are very helpful when troubleshooting or submitting a big report.

```bash
go build -ldflags "-s -w" -o sim-engine main.go
```

**Running the Sim engine**
You will need to set the URI of the RabbitMQ instance as an environment variable before proceeding, if you are running the default RabbitMQ setup on the same device you can use the following:

```bash
RMQ_URI=amqp://guest:guest@localhost:5672
```

Be sure to replace guest:guest with the username:password you set if it is different, similarly changing :5672 to :##### of the port you set (if changed), finally changing localhost to the IP address of the device running RabbitMQ, if you are unsure how to do this you can find some instructions [here](https://www.avast.com/c-how-to-find-ip-address).

**Note:** Attempting to run the Sim Engine without RabbitMQ running will give errors as it cannot communicate and create the messaging constructs needed

You can run an instance of the Sim Engine as you would any other executable. Below is the command to run whilst in the same folder as the executable.

```bash
./sim-engine
```

You can append an ampersand '&' to the end of this to run it in the background, this could be useful if you want to run many, though you will no longer see info as it runs.

#### <ins>RabbitMQ<ins/>

You can run RabbitMQ however works for your use case, as long as it is accessible to the API server and Sim engine instances, instructions for installing RabbitMQ can be found [here](https://www.rabbitmq.com/docs/download). You can find information regarding managing RabbitMQ [here](https://www.rabbitmq.com/docs/manage-rabbitmq).

### Organisation Guide

As an organisation looking to serve the app to multiple users you can either follow the basic steps for a single user, installing the whole stack on a single device or have a more distributed setup based on your architecture.

If you decide to use the single user setup, be sure to edit the Docker Compose and network settings of your device to allow other clients on your network to access the container. The Spring instance serves on port 8080, this can be mapped to another port outside the container if needed/wanted.

Alternatively, it may be better to use a more distributed architecture, we would recommend running the Spring Api-Server and RabbitMQ instance on the same machine, with the Sim-Server instances running on their own machines, ensure the network setup allows the Sim-Servers to access the RabbitMQ instance. Running multiple Sim-Server instances on a single machine can help with availability, however ensure there is enough compute to drive all instances, the compute limit is the main reason to distribute the system.

The architecture used can change across organisations, using Docker (Swarm), Kubernetes, Cloud Compute or just building and running on multiple servers. The main requirement is that all Sim-Server instances can talk to RabbitMQ, and the Api-Server can talk to RabbitMQ, serve it's content and support websocket connections. By default RabbitMQ uses port 5672 and Spring uses port 8080.

You may also want to setup an on-prem DNS record to point to the Api-Server for ease of user access, along with generating and setting up SSL certs to allow for https and wss connections.

## User Maunal

### Synopsis

You have been informed that a disease has broken out in your country and the government has chosen you to lead the epidemic response team. Your goal is to stop the spread of the disease, while limiting the damage the disease does, both economically and by number of dead. You have to manage your resources wisely to best combat the epidemic. Be warned the infection rates you are aware of are not necessarily the real infection rates. To better understand the disease, you must invest in testing. If you manage to stop the disease from spreading you have completed your task and have won the game, but at what cost? You can see after the game the rate of spread, the number of dead and the GDP impact of the epidemic as well as how your actions impacted these. Learn from your mistakes and successes to improve your strategies for next time you play.

### Controls

![image](Screenshot1.png)
![image](Screenshot2.png)
![image](Screenshot3.png)

1. Start game button: Press to start the game
2. Social policy button: Not currently implemented
3. Upgrade infrastructure button: Not currently implemented
4. Apply mask mandate button: Applies mask mandate to selected jurisdiction. If no jurisdiction is selected mask mandate is applied everywhere. Mask mandate reduces the emissions of infections vectors, thus lowering the risks of the disease spreading.
5. Lockdown button: Applies lockdown to selected jurisdiction. If no jurisdiction is selected lockdown is applied everywhere. Lockdown stops all movement, but it still allows agents to return to their homes.
6. Metrics: Different statistics you can check to see how the epidemic is progressing and how and some areas you might want to focus on.
7. Overviews: Different overviews for you to look through, currently only the map view is implemented.
8. Main Map: Shows the area that the game is taking place. The brighter red an area is the greater the number of infectioned there.
9. Pause/Play button: Press to pause the game and restart the game.
10. Quit game button: Press to exit current itteration of game.
11. Local Authority Districts (LADs): The middle layer jurisidiction.
12. Middle layer Super Output Areas (MSOAs): The lowest layer jurisdiction.
13. Resources: This is the remaining budget you have. Be carful not to run out.
14. Oracle: The Oracle will pop up to help you. You can dismiss it by pressing th button.

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

We have two Controller classes, again in an aptly named Package. The base Controller contains a simple root redirect to the static html of the UI, and a messaging endpoint to recieve the Game Command messages via STOMP. These commands are then forwarded over Rabbit. The other Controller Class contains the game creation endpoint, it creates a generic setup and attemps to serialise and send the appropriate data over Rabbit to a simulation engine instance and back as a response to the POST request to the client.

The Repository Package contains several Records used simply as skeletons for (de)serialising messages, either from Rabbit or from STOMP.

The final Package is Services, which contains a single service currently which is responsible for listening to a given RabbitMQ queue (game-metrics in this case) and do some processing, here it simply serialises the Metrics Map and forwards the data to the appropriate client using STOMP.

There are no static resources stored in the Api-Server repository, as all frontend development is done in the UI repo. This is then built and exported as a set of static resources which can be placed in the Api Server's static folder and built into the jar for serving to clients.

### Simulation Engine - [Repo Link](https://github.com/CoralCoralCoralCoral/simulation-engine)

You can run the Simulation engine during development by following the instructions to build the Sim Engine, and use the below command instead of the build command.

```bash
go run main.go
```

Instead of setting the RabbitMQ URI as an environment variable you can also use the same syntax as the build guide but in a file called '.env' in the same folder as the rest of the source files/executable using the flag `--dev`, i.e.

```bash
go run main.go --dev
```

Currently the only change to using this flag is sourcing the RabbitMQ URI from the .env file instead of an environment variable, this flag will cause the program to crash if the file is not present or the URI is incorrect, in the same way not setting or incorrectly setting the RMQ_URI environment variable would.

### Contributing to the Simulation Engine

The simulation engine is the single most important piece of software that lives at the heart of our game. Without this repository, there is no game. This is a guide dedicated to engineers looking to contribute to the development of the simulation engine. This guide is also for you if you simply want to fork this repository and modify it for your own use. This guide will lay out the fundamental abstractions we have relied on during the development of the most definitive features of the engine. Without further ado, let's dive into it!

#### A note on directory structure

Since the simulation engine is written in Go, we would like to take this opportunity to remind the user that we have adhered to Go's idiomatic folder structuring practices. That is, each folder within the root directory is considered its own package. Files within each package all share the same namespace. This comes with the added convenience that types defined in a file `a.go` are all accessible from any other file `b.go` within the same package without the need for any import statements.

With that said, we have tried our best to keep the components of the simulation engine as modular as possible. Where appropriate, we have split functionality up into different packages, in the spirit of maintaining a clear separation of concerns.

The simulation engine is comprised of the following packages:

-   model
-   logger
-   messaging
-   geo

#### The `model` package

This is a package that encapsulates the logic of the agent-based simulation model we built for the game. This package is designed to be a library that is consumed by a higher level consumer such as a binary package that composes an application together using the `model` package to generate real-time simulations of epidemics. The purpose of this package is thus to expose a standard API with which to read data from and interact with a real-time, agent-based epidemici model. This package has no internal dependencies other than the `logger` and `geo` packages (also defined in this repository). The `geo` package is a dependency only insofar as it is needed for the default implementation of the `EntityGenerator` interface (which we will get into shortly).

##### The `Config` type

The `Config` type encapsulates all of the parameters of the simulated epidemic that we currently allow the consumer to set. We currently support the following parameters to be set via `Config`:

```go
type Config struct {
    // A UUID supplied externally by the consumer to be used as the simulation ID
	Id        uuid.UUID `json:"id"`

    // The most atomic in-game timestep the model will simulate, in milliseconds
	TimeStep  int64     `json:"time_step"`

    // The total number of agents to be modelled
	NumAgents int64     `json:"num_agents"`

    // The pathogen to be modelled (more details below)
	Pathogen  Pathogen  `json:"pathogen"`
}

type Pathogen struct {
    // the distribution of the incubation period of the pathogen, in milliseconds
	IncubationPeriod           [2]float64 `json:"incubation_period"`

    // the distribution of the recovery period of the pathogen, in milliseconds
    RecoveryPeriod             [2]float64 `json:"recovery_period"`

    // the distribution of the immunity period of the pathogen, in milliseconds
    ImmunityPeriod             [2]float64 `json:"immunity_period"`

    // given that an agent will be hospitalized, the distribution of the pre-hospitalization period, in milliseconds
	PrehospitalizationPeriod   [2]float64 `json:"prehospitalization_period"`

    // given that an agent will be hospitalized, the distribution of the hospitalization period, in milliseconds
	HospitalizationPeriod      [2]float64 `json:"hospitalization_period"`

    // the distribution of the quanta emission rate of an infectious individual (quanta per hour; see Wells-Riley model for details)
	QuantaEmissionRate         [2]float64 `json:"quanta_emission_rate"`

    // the independent probability that an infected individual will become hospitalized
    HospitalizationProbability float64    `json:"hospitalization_probability"`

    // the probability that death will occur in an infected individual given that they are hospitalized (conditional on hospitalized)
	DeathProbability           float64    `json:"death_probability"`

    // the probability that an infected individual remains asymptomatic upon becoming infectious
	AsymptomaticProbability    float64    `json:"asymptomatic_probability"`
}
```

##### Model Entities

The epidemic simulation model essentially deals with the following entities:

-   `Agent`
-   `Space`
-   `Jurisdiction`

**Agent**: represents an individual person in the model and they belong to a `household`, which is a `Space`.
`Agent`s also have a designated `office`, which is also a `Space`. In addition to these, an `Agent` has a set of designated `social_spaces` they can visit, as well as a set of `healthcare_spaces` where they are likely to seek and receive treatment. An agent's `healthcare_spaces` and `social_spaces`, as the name suggests, are all of type `Space`. Since `Agent`s are allowed to move between spaces in this model (afterall, what is an epidemic model that doesn't take into account movement), each agent has a `location` attribute, which always tracks the agent's current location throughout the model.

Equally crucial is that agents can be in one of the following infection states at any given time:

-   `Susceptible`
-   `Infected`
-   `Infectious`
-   `Immune`
-   `Hospitalized`
-   `Dead`

Agents transition through these states as the simulation progresses over time, according to the [SEIRS model](https://www.nature.com/articles/s41592-020-0856-2).

Furthermore, since we model transmission via the airborne route using a discretized version of the [Wells-Riley model](https://en.wikipedia.org/wiki/Wells-Riley_model), agents have an associated `pulmonary_ventilation_rate`, which combined with the `quanta_emission_rate` of the pathogen makes up the transmission vector in this model.

**Space**: represents a physical space that can house zero or more `Agent`s at any given time. Spaces have a `volume` associated with them, an `air_change_rate`, and an attribute called `total_infectious_doses`. The simulation model tracks the `total_infectious_doses`, assumed to be mixed uniformly with the air, as a function of infectious occupants breathing out infectious quanta, the `volume` of the space and the `air_change_rate`.

Each space belongs to a `Jurisdiction`, from which it inherits a notion of geo-spatial position, and through which a player may target spaces by applying surveillance and infection control policies to jurisdictions.

**Jurisdiction**: represents, as the name suggests, geographically bounded administrative areas within which specific surveillance and infection control policies may be applied. As a major objective of the game is to be able to efficiently stop an ongoing epidemic, we want the user be able to realistically consider policy decisions that can be applied per administrative area. Jurisdictions do not necessarily have a strict hierarchy, although they may be used to model real-life administrative hierarchies such as that between Local Authority Districts and MSOAs in the UK. To allow arbitrary hierarchies, jurisdictions can have parent-child relationships, and can form trees with infinitely many levels.

Jurisdictions have an attribute called `feature`, which allows us to associate with it a geojson feature, such as a polygon that corresponds to the boundaries of a given administrative area. This allows for geo-spatial visualization of the epidemic state as we do in our game.

##### The `EntityGenerator` interface

Before we can start modelling an epidemic, we need some agents to simulate, some spaces between which they will move, and some jurisdictions within which each space would reside. This is the role of the `EntityGenerator`. The accuracy of the simulated model is only as good as how realistic the generated entities are. The `EntityGenerator` is a simple Go interface that defines a method called `Generate`:

```go
type EntityGenerator interface {
	Generate(config *Config) Entities
}

type Entities struct {
	agents            []*Agent
	jurisdictions     []*Jurisdiction
	households        []*Space
	offices           []*Space
	social_spaces     []*Space
	healthcare_spaces []*Space
}

```

The `Generate` method takes a `Config` as its only argument and returns a struct of type `Entities`. This is a crucial interface responsible for initializing the agents, jurisdictions, spaces and the relationships between them. We have abstracted this function away in an interface so that it would be straightforward to plug in custom entity generators. The `Entities` type includes the following as its members:

-   agents (of type `Agent`)
-   jurisdictions (of type `Jurisdiction`)
-   households (of type `Space`)
-   offices (of type `Space`)
-   social_spaces (of type `Space`)
-   healthcare_spaces (of type `Space`)

These are all passed to the `Simulation` instance before the model is started.

###### The `DefaultEntityGenerator`

We provide a default entity generator that includes all LADs and MSOAs within the Greater London Area. The `DefaultEntityGenerator` also allocates `Jurisdictions` to all of the generated `Spaces` according to the population density of each MSOA. This data was obtained via the Office for National Statistics. The preprocessing for creating `Jurisdictions` out of the London LADs and MSOAs are all contained within the `geo` package.

##### The `Simulation` Type

`Simulation` is a type that contains all of a simulation's state, including all agents, spaces, jurisdictions, pause_state, and other control states of the simulation.
The simulation runs a forever loop that uses a go switch to switch between receiving a `Command` message from a go channel, in which case it would call its `processCommand` method, or if there is no `Command` pending, call its `simulateEpoch` method.
`simulateEpoch` is the main method that runs during each simulation step.

###### The `simulateEpoch` method

This method does three things:

1. increments the current epoch by 1
1. for each agent in the simulation, calls its respective `update` method
1. for each space in the simulation, calls its respective `update` method

###### The `processCommand` method

This is a method on the simulation that processes commands received from the user, and applies them to the simulation, causing side-effects to the simulation state.
Once a command is processed, the simulation logs a `CommandProcessed` event.

###### The `Policy` Type

Policies are associated with jurisdictions and contain information on what actions (surveillance or intervention) have been applied to a jurisdiction, as part of the effort to try and contain the epidemic.
The current policy actions players can implement are as follows:

```go
type Policy struct {
	// tracks whether a mask mandate is in effect in the jurisdiction
	is_mask_mandate          bool

	// tracks whether a lockdown is in effect
	is_lockdown              bool

	// this applies only to healthcare spaces
	// and tracks the current test strategy applied to it.
	// it can be one of "test_everyone", "test_none" and "test_symptomatic"
	test_strategy            TestStrategy

	// this applies only to healthcare spaces and tracks
	// if a multiplier has been applied to a jurisdiction's healthcare spaces' test capacity.
	// this is an action that would typically be used once a jurisdiction
	// starts accumulating a test backlog due to a surge in infections
	test_capacity_multiplier float64
}
```

###### `Commands`

`Commands` are messages a user can send to interact with the simulation state.
Commands have a `Type` and `Payload`. The payload of each command depends on its type. It is possible that some commands may not have an associated `Payload`, such as `Quit` or `Pause` commands.

Please see [model/command.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/command.go) to see a list of implemented commands

`Commands` are designed to be extendable such that whenever a new type of user interaction is desired, it's simply a matter of declaring a new type of command and an associated payload type, if required.
When extending `Commands`, the implementor must also edit the `Simulation `'s `processCommand` method to include the new command type in the switch-case handler, where the implementer would apply handling logic for the new case as desired.

Currently, the user can implement surveillance and intervention actions by sending an `ApplyPolicyUpdate` command. This is a command that allows users to apply partial updates to a targeted jurisdiction's `Policy`, which would also apply recursively to the jurisdiction's children's policies.
For example, if a Lockdown is applied to a Jurisdiction that represents a Local Authority District (LAD), the policies associated with all of the MSOAs within the targetted LAD will also reflect that a lockdown has been applied.

```go
	apply_lockdown := true
	apply_lockdown_command := Command {
		Type: ApplyPolicyUpdate,
		Payload: &ApplyPolicyUpdatePayload {
			// select
			IsLockdown: &apply_lockdown
		}
	}
```

###### The `Logger` and `Events`

The simulation also logs important `Event`s that occur within the model to a `Logger` instance that is part of the `Simulation` state.
Similar to `Commands`, events have a `Type` and optional `Payload`.

The simulation instance provides a convenience method to the consumer called `Subscribe`, that allows consumer code to hook into this event stream. The signature for the `Subscribe` method is as follows:

```go
func Subscribe(subscriber func(event *logger.Event))
```

where `subscriber` is a closure the consumer provides, which receives every event sequentially. As you can see, the proper type of the event is `*logger.Event`, which implies that the consumer receives a reference to the event, and that furthermore, the logger is a package that is external to the `model` package. This was a deliberate design decision to keep the `logger` logic separate from the `model` package, while allowing `model` as well as the customer's calling code to be able to depend on it.

Please see [model/events.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/events.go) to see a list of already implemented events.

Similar to commands, `Events` are designed to be extendable such that whenever a new process is introduced within the model, you may log your newly defined events using the simulation's logger.

###### Implementing New Processes

When implementing new processes, the consumer will most likely want to restrict their modifications to the following files:

-   [model/agent.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/agent.go)
-   [model/space.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/space.go)
-   [model/policy.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/policy.go)

If the consumer would like to modify the way agents transition through infection states or modify agent's movement patterns, please refer to methods defined under `Agent` in "model/agent.go".
If the consumer would like to modify the way space state transitions occur, please refer to methods defined under `Space` in "model/space.go".
If the consumer would like to modify the way policies work, or potentially add new policy actions, please modify the `Policy` type in "model/policy.go". If adding new policies, the consumer would also need to modify the associated `PolicyUpdatePayload`, which is sent as part of the `PolicyUpdate` event.

### UI - [Repo Link](https://github.com/CoralCoralCoralCoral/ui)

To run the UI in development mode you can follow the instructions to build the UI from source but replace the final `npm run build` command with `npm run dev` which will host the UI at http://localhost:3000/.
The Api Server is setup so CORS should not block requests from this development server meaning you do not have to fully rebuild the UI into static content and bundle it into the Api Server to run or build just to test a UI change.

You can also set the MapBox API key in a file, using the same syntax as setting the environment variable in a file named .env(.local) in the build folder.
**Note:** Be sure not to commit the file to any source control system.

#### File Structure Overview

**app** - contains the different pages, layout doc, global css doc and the fonts used.
**api** - handlers for API routes.
**components\ui** - reuseable UI components.
**store** - contains the different slices of store along with the respecitve reducers. 

#### GameProvider
This is a context provider which wraps the entire application and injects the game context into the app.

The game provider provides the following control functions and state via the `useGameContext` hook, which allows any component rendered within the GameProvider's tree to start, pause and resume simulations, along with a few additional state variable and methods.

```ts
import { useGameContext } from "@/game/GameContext"

const ExampleComponentWithinGameProviderTree = () => {

    const {
        error,
        isLoading,
        isConnected,
        isInitialized,
        isPaused,
        gameId,
        sendCommand,
        startGame,
        pauseGame,
        resumeGame
    } = useGameContext()

    return <div>This is a Demo Component!</div>
}

```

The GameProvider handles all the logic of setting up bidirectional messaging between the client and the simulation engine over websockets.

All of this logic lives inside the root level `game` directory.

This component depends on the availability of a metrics and policy store (already configured), which it will update based on event and metrics messages received from the simulation-engine.

#### GameMap

This is a component that renders a map of the area in focus. The behaviour of the gameMap can be modified via `components/ui/gameMap.tsx`. The default behaviour of the map is such that it focuses in on the currently selected `jurisdiction` as tracked by the `navigation` slice of the applicaton's main redux store.

#### Oracle

The Oracle is a component located at `components/ui/Oracle.tsx`

This component currently implements a basic Oracle, that listens to real-time metrics updates (by hooking into the metrics store), and works by way of a set of triggers.

The current behaviour of the Oracle is the following:
- Interrupts the gameplay, pauses the game and appears as a Dialog warning the user of the event that triggered it.
- The Oracle gets triggered whenever either a new infection is recorded for the first time in any given Local Authority District (LAD), or whenver the first death has occured in any given LAD.

New triggers can be implemented for the Oracle by following the reference implementation.

### RabbitMQ

We use RabbitMQ as a messaging service between the API Server and any number of Simulation Engine instances. 

#### Topology

It currently handles three main message types:

- Init Game: Sent from the API Server to an Available Sim Engine instance
  - The message contains config information for the simulation to run
  - There is one Exchange in topic mode connected to one Queue, many Sim engine instances can subscribe to the same queue with message distribution being handled by Rabbit
- Game Notifications: Sent from a Simulation running in a Sim engine instance to the API Server
  - Messages can be of a few types, daily aggregate metrics about infections etc, policy applied on a juristiction, and a message to signify simulation initialisation is complete
  - There is one Exchange in topic mode connected to a Queue, one API server is subscribed to the Queue, the routing key is the following (`API-UUID` being the API Server UUID) `API-UUID.*`
- Game Commands: Sent from the API Server to a Simulation in a Sim engine
  - Messages contain a command type and optional payload which contains extra data, i.e. a pause command would not contain a payload but a policy application would contain the policy type and the juristiction it is applied to
  - There is one Exchange in topic mode connected to many Queues, each simulation will create a Queue it consumes from using the routing key in the following form (`SIM-UUID` being the Simulation UUID) `*.SIM-UUID`. One Sim engine instance may run many simulations with many attached Queues

#### Online Docs

The RabbitMQ docs are very informative, with examples in many popular languages, including Go and Java (the two used in this project that interact with RabbitMQ), click [here](https://www.rabbitmq.com/docs) to access the start of the RabbitMQ docs. A quick web search for "Rabbit x" will often be enough to find an example of what you want.

#### Web Management console

A helpful tool when developing or debugging the project is the RabbitMQ management portal. When you run the appropriate Rabbit version (which we use in the Docker Compose file), you can access the management portal at http://localhost:15672/ using the set username and password, by default those are 'guest' and 'guest'.

From there you can view the setup Exchanges, which queues are defined, where they are attached and with which routing keys. You can also view message statistics and manually dispatch messages to a queue or exchange. More infomation regarding this is available [here](https://www.rabbitmq.com/docs/management).
