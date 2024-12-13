# Contributing to the Simulation Engine

The simulation engine is the single most important piece of software that lives at the heart of our game. Without this repository, there is no game. This is a guide dedicated to engineers looking to contribute to the development of the simulation engine. This guide is also for you if you simply want to fork this repository and modify it for your own use. This guide will lay out the fundamental abstractions we have relied on during the development of the most definitive features of the engine. Without further ado, let's dive into it!

## A note on directory structure

Since the simulation engine is written in Go, we would like to take this opportunity to remind the user that we have adhered to Go's idiomatic folder structuring practices. That is, each folder within the root directory is considered its own package. Files within each package all share the same namespace. This comes with the added convenience that types defined in a file `a.go` are all accessible from any other file `b.go` within the same package without the need for any import statements.

With that said, we have tried our best to keep the components of the simulation engine as modular as possible. Where appropriate, we have split functionality up into different packages, in the spirit of maintaining a clear separation of concerns.

The simulation engine is comprised of the following packages:

-   model
-   logger
-   messaging
-   geo

## The `model` package

This is a package that encapsulates the logic of the agent-based simulation model we built for the game. This package is designed to be a library that is consumed by a higher level consumer such as a binary package that composes an application together using the `model` package to generate real-time simulations of epidemics. The purpose of this package is thus to expose a standard API with which to read data from and interact with a real-time, agent-based epidemici model. This package has no internal dependencies other than the `logger` and `geo` packages (also defined in this repository). The `geo` package is a dependency only insofar as it is needed for the default implementation of the `EntityGenerator` interface (which we will get into shortly).

### The `Config` type

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

### Model Entities

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

### The `EntityGenerator` interface

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

#### The `DefaultEntityGenerator`

We provide a default entity generator that includes all LADs and MSOAs within the Greater London Area. The `DefaultEntityGenerator` also allocates `Jurisdictions` to all of the generated `Spaces` according to the population density of each MSOA. This data was obtained via the Office for National Statistics. The preprocessing for creating `Jurisdictions` out of the London LADs and MSOAs are all contained within the `geo` package.

### The `Simulation` Type

`Simulation` is a type that contains all of a simulation's state, including all agents, spaces, jurisdictions, pause_state, and other control states of the simulation.
The simulation runs a forever loop that uses a go switch to switch between receiving a `Command` message from a go channel, in which case it would call its `processCommand` method, or if there is no `Command` pending, call its `simulateEpoch` method.
`simulateEpoch` is the main method that runs during each simulation step.

#### The `simulateEpoch` method

This method does three things:

1. increments the current epoch by 1
1. for each agent in the simulation, calls its respective `update` method
1. for each space in the simulation, calls its respective `update` method

#### The `processCommand` method

This is a method on the simulation that processes commands received from the user, and applies them to the simulation, causing side-effects to the simulation state.
Once a command is processed, the simulation logs a `CommandProcessed` event.

#### The `Policy` Type

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

#### `Commands`

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

#### The `Logger` and `Events`

The simulation also logs important `Event`s that occur within the model to a `Logger` instance that is part of the `Simulation` state.
Similar to `Commands`, events have a `Type` and optional `Payload`.

The simulation instance provides a convenience method to the consumer called `Subscribe`, that allows consumer code to hook into this event stream. The signature for the `Subscribe` method is as follows:

```go
func Subscribe(subscriber func(event *logger.Event))
```

where `subscriber` is a closure the consumer provides, which receives every event sequentially. As you can see, the proper type of the event is `*logger.Event`, which implies that the consumer receives a reference to the event, and that furthermore, the logger is a package that is external to the `model` package. This was a deliberate design decision to keep the `logger` logic separate from the `model` package, while allowing `model` as well as the customer's calling code to be able to depend on it.

Please see [model/events.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/events.go) to see a list of already implemented events.

Similar to commands, `Events` are designed to be extendable such that whenever a new process is introduced within the model, you may log your newly defined events using the simulation's logger.

#### Implementing New Processes

When implementing new processes, the consumer will most likely want to restrict their modifications to the following files:

-   [model/agent.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/agent.go)
-   [model/space.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/space.go)
-   [model/policy.go](https://github.com/CoralCoralCoralCoral/simulation-engine/blob/main/model/policy.go)

If the consumer would like to modify the way agents transition through infection states or modify agent's movement patterns, please refer to methods defined under `Agent` in "model/agent.go".
If the consumer would like to modify the way space state transitions occur, please refer to methods defined under `Space` in "model/space.go".
If the consumer would like to modify the way policies work, or potentially add new policy actions, please modify the `Policy` type in "model/policy.go". If adding new policies, the consumer would also need to modify the associated `PolicyUpdatePayload`, which is sent as part of the `PolicyUpdate` event.
