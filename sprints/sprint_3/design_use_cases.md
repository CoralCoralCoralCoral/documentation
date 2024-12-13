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

### Tests

1. Test that Logger receives and publishes events correctly

    - add new logger subscriber, with a closured callback listening to expected messages
    - log expected messages to the logger
    - inside the listener callback, assert that expected messages arrive in the correct order

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

### Tests

1. Test that InitRx receives init messages from remote endpoint

    - create new InitRx
    - attach closured callback function to the receiver by calling the OnReceive method
    - send an init message to the queue init receiver is listening on
    - assert that the closured callback function receives the init message as expected

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

### Tests

1. Test that CommandRx receives command messages from remote endpoint

    - create new CommandRx
    - attach closured callback function to the receiver by calling the OnReceive method
    - send an command message to the queue command receiver is listening on
    - assert that the closured callback function receives the command message as expected

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

### Tests

1. Test that MetricsTx transmits command messages to remote endpoint

    - create new MetrixTx bound to a test queue
    - create a mock remote endpoint that consumes from a test queue that metrics tx will publish to
    - send a metrics message to the test queue
    - assert that the mock remote endpoint receives the metrics message as expected

## D10 (v1)

1. **Title**: Create Game
2. **Purpose**: Allow a User to create and start a new simulation
3. **Actors**: Api Server, UI, User
4. **Preconditions**:
    - Rabbit is running and connected to API server
    - API Server is running and served frontend UI to user
5. **Main Flow**:
    - User presses Start Game button
    - UI provides simulation config options
    - UI sends POST request to API Server with the config
    - API Server generates Game UUID
    - API Server receives Init Sim request and forwards to appropriate Rabbit queue along with generated UUID
    - API Server responds to POST request with generated UUID
    - UI initialises a websocket connection and listens to appropriate STOMP endpoints based on UUID
6. **Postcondition**:
    - The init game Rabbit Exchange has received a message to pass to an eligible Sim Engine instance
    - The UI has received the simulation UUID
    - The UI and Api Server are connected via Websocket and STOMP endpoint subscription setup

### Tests

1. Test API server correctly handles receives Create Game message
    - create required Rabbit structures (Exchanges/Queues)
    - Click (Mock) Start Game button
    - API Server receives message
    - Assert message is forwarded to Rabbit
    - Assert response is sent to client

## D11 (v1)

1. **Title**: Manage game messages
2. **Purpose**: Connect a Sim engine instance to the UI displayed to a User
3. **Actors**: Api Server
4. **Preconditions**:
    - A game has been created and UI is using STOMP via connected websocket
    - RabbitMQ is running and connected to API Server
5. **Main Flow**:
    - API Server listens to the appropriate Rabbit Queue for game metrics and when a message is received forward via a STOMP endpoint using the sim UUID
    - API Server listens to game commands STOMP endpoint and forwards message to appropriate Rabbit Exchange using sim UUID
6. **Postcondition**:
    - Game metrics messages are forwarded to UI
    - Game command messages are forwarded to Sim via Rabbit

### Tests

1. Test Metrics messages are consumed from Rabbit and sent to UI
    - create required Rabbit structures (Exchanges/Queues)
    - mock a metrics message in the appropriate queue
    - assert message is consumed and received by UI

2. Test Command messages are received and sent to Rabbit
    - create required Rabbit structures (Exchanges/Queues)
    - mock a command sent to command STOMP endpoint
    - assert message is sent to appropriate Rabbit queue


## D3 (v2) [Updated from D3 (v1)]

1. **Title**: Agent infection state update subroutine
2. **Purpose**: To simulate an agent's infection state transition within a single time step of the simulation
3. **Associated User Stories**:
4. **Associated Use Cases**: D2 (v1)
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
    - _if the agent's infection state has changed, log an `AgentStateUpdate` event_

### Tests

1. Test that agent state updates correctly

    - initialize agent in a known state with a known transition duration
    - call agent state update with mock simulator instance, each time advancing the epoch until known duration is reached
    - assert that agent state transitioned to new expected state
    - repeat above for every possible state transition

## D4 (v2) [Updated from D4 (v1)]

1. **Title**: Agent location update subroutine
2. **Purpose**: To simulate movement of an agent within a single timestep of the simulation
3. **Associated User Stories**:
4. **Associated Use Cases**: D2 (v1)
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
    - _if the agent's location has changed, log an `AgentLocationUpdate` event_

### Tests

1. Test that agent location updates correctly

    - initialize agent in a known location with a known next_move_epoch
    - call agent state update with mock simulator instance, each time advancing the epoch until known next_move_epoch is reached
    - assert that agent location transitioned to new expected location (this is not deterministic, as next location is determined randomly, but maybe can be tested using a seeded RNG)
