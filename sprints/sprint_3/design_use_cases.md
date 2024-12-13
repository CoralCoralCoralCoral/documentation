# Design Use Cases

## D6 (v1)

1. **Title**: Logger
2. **Purpose**: To log all simulation state changes as events and allow other processes to subscribe to these events and perform tasks such as metrics aggregation, event forwarding to external systems, etc.
3. **Actors**: Simulation Engine
4. **Preconditions**:
    - The main simulation loop is running
5. **Main Flow**:
    - a subroutine within a simulation calls the `log` method to send an event of a specific type with an optional payload to the logger
    - the logger broadcasts the event to all currently attached subscriber processes (processes that are running in their own green thread (go-routine) and thus external to the simulation)
6. **Alternative Flow**:
    - an external process attaches a subscriber to the logger, supplying a closured callback function to be called when an event is received by the logger
    - the logger calls all attached callback functions with events as they arrive
7. **Postcondition**:
    - There are no side-effects (as far as the simulation is concerned) from either of these flows

## D7 (v1)

1. **Title**: Init Receiver (InitRx)
2. **Purpose**: To allow a remote endpoint to start a new simulation
3. **Actors**: Simulation Engine, Remote Endpoint
4. **Preconditions**:
    - The simulation engine is connected to a message queue service such as RabbitMQ
5. **Main Flow**:
    - Remote endpoint publishes a new init message to the init queue
    - The simulation engine reads the message from the init queue
    - The simulation engine deserializes the init message into a simulation `Config`
    - The simulation engine starts a new simulation with the provided `Config`
    - The simulation engine attaches a metrics transmitter to the simulation instance (to forward aggregated metrics to the remote endpoint)
    - The simulation engine attaches a command receiver to the simulation instance (so that the remote endpoint can send commands to the simulation and interact with it)
6. **Alternative Flow**:
    - the remote endpoint sends an invalid init message
    - the simulation engine silently drops the message and continues
7. **Postcondition**:
    - A new simulation instance is running

## D8 (v1)

1. **Title**: Command Receiver (CommandRx)
2. **Purpose**: To allow remote endpoints to send command messages to a specific simulation instance
3. **Actors**: Simulation Engine, Remote Endpoint
4. **Preconditions**:
    - The simulation engine is connected to a message queue service such as RabbitMQ
    - The command receiver is attached to a running simulation
5. **Main Flow**:
    - Remote endpoint sends a command message
    - the command receiver deserializes the message into a `Command`
    - the command receiver forwards the `Command` to the simulation it is attached to
    - The simulation processes the `Command`
    - The simulation publishes a `CommandProcessed` event
6. **Alternative Flow**:
    - the remote endpoint publishes an invalid command message
    - the simulation engine silently drops the message and continues
7. **Postcondition**:
    - Some side-effects may have been applied as a result of the simulation processing the `Command`

## D9 (v1)

1. **Title**: Metrics Transmitter (MetricsTx)
2. **Purpose**: To forward metrics aggregated from a simulation's event log to remote endpoints
3. **Actors**: Simulation Engine, Remote Endpoint
4. **Preconditions**:
    - The simulation engine is connected to a message queue service such as RabbitMQ
    - The metrics transmitter is subscribed to the running simulation's event log
5. **Main Flow**:
    - The simulation instance produces events to the log
    - the metrics transmitter aggregates events for each in-game day
    - the metrics transmitter sends a `Metrics` message at the end of each in-game day
    - the remote endpoint receives the aggregated metrics
6. **Postcondition**:
    - There are no side-effects from this flow

## D3 (v2) [[Updated from D3 (v1)]](../sprint_2/design_use_cases.md)

1. **Title**: Agent infection state update subroutine
2. **Purpose**: To simulate an agent's infection state transition within a single time step of the simulation
3. **Associated User Stories**: [3](../sprint_1/user_stories.md)
4. **Associated Use Cases**: D2
5. **Actors**: Simulation Engine
6. **Preconditions**:
    - The main simulation loop is running
7. **Main Flow**: Agent is in the `Susceptible` state
    - calculate the probability of being infected based on the Wells-Riley model of airborne transmission
    - sample from the Bernoulli distribution using the result from the previous step to determine if the agent should transition to the `Infected` state
    - if the result of the previous step is 1, then transition the agent state to `Infected`
    - generate an infection profile for the agent (based on the pathogen profile) and associate it with the agent. The infection profile contains details like the incubation period for this instance of infection, whether or not the agent will eventually be hospitalized, whether or not the agent will eventually die, etc.
8. **Alternative Flow 1**: Agent is in the `Infected` state
    - if the duration between when the agent became infected and the current epoch is greater than or equal to the agent's incubation period, update the state to `Infectious`
    - if the duration between when the agent became infected and the current epoch is less than the incubation period, return
9. **Alternative Flow 2**: Agent is in the `Infectious` state
    - if according to the infection profile, the agent gets hospitalized
      and the duration between the current epoch and when the agent became infectious is greater than or equal to the agent's pre-hospitalization period, update the agent's state to `Hospitalized`
    - else if the duration between when the agent became infectious and the current epoch is greater than or equal to the agent's recovery period, update the agent state to `Immune`
    - else, return
10. **Alternative Flow 3**: Agent is in the `Hospitalized` state
    - if according to the infection profile, the agent dies
      and the duration between the current epoch and when the agent became hospitalized is greater than or equal to the agent's hospitalization period, update the agent's state to `Dead`
    - else if the duration between when the agent became hospitalized and the current epoch is greater than or equal to the agent's hospitalization period, update the agent state to `Immune`
    - else, return
11. **Alternative Flow 4**: Agent is in the `Immune` state
    - if the duration between when the agent became immune and the current epoch is greater than or equal to the agent's immunity period, update the agent state to `Susceptible`
    - else, return
12. **Alternative Flow 5**: Agent is in the `Dead` state
    - this is a noop, return
13. **Post Condition**:
    - the agent's infection state has potentially been updated
    - if the agent's infection state has changed, log an `AgentStateUpdate` event

## D4 (v2) [[Updated from D4 (v1)]](../sprint_2/design_use_cases.md)

1. **Title**: Agent location update subroutine
2. **Purpose**: To simulate movement of an agent within a single timestep of the simulation
3. **Associated User Stories**:
4. **Associated Use Cases**: D2
5. **Actors**: Simulation Engine
6. **Preconditions**:
    - The main simulation loop is running
7. **Main Flow**: agent is in the household
    - if agent's `next_move_epoch` is less than the current epoch, return
    - flip a coin to determine if the agent will go to the office
      or a randomly selected social space nearby, using a hardcoded probability.
    - if the agent goes to the office, set the `next_move_epoch` to the current epoch +
      a duration randomly sampled from a normal distribution of expected durations spent in the office
    - if the agent goes to a social space, set the `next_move_epoch` to the current epoch +
      a duration randomly sampled from a normal distribution of expected durations spent in social spaces
8. **Alternative Flow 1**: agent is in the office or a social space
    - update agent's location to the household
    - set the `next_move_epoch` to the current epoch +
      a duration randomly sampled from a normal distribution of expected durations spent in the household
9. **Alternative Flow 2**:
    - if agent is in the `Hospitalized` state and agent's state changed in the current epoch, change the agent's location to a random healthcare space nearby
    - set the `next_move_epoch` to the curernt epoch + the agent's hospitalization_period
10. **Alternative Flow 3**:
    - if agent is in the `Infectious` state and agent's state changed in the current epoch, and the agent is symptomatic and seeks treatment, change the agent's location to a random healthcare space nearby
    - set the `next_move_epoch` to the current epoch + a duration sampled randomly from a normal distribution of expected durations spent seeking treatment in healthcare spaces
11. **Post Condition**:
    - the agent's location has potentially been updated
    - if the agent's location has changed, log an `AgentLocationUpdate` event
