# Design Use Cases

## D1 (v1) [[User Story 3 (v1)]](../sprint_1/use_cases.md)

1. **Title**: Main simulation loop
2. **Purpose**: To simulate a model in which agents move between spaces over time
3. **Associated User Stories**: 3 (v1)
4. **Actors**: Simulation Engine
5. **Preconditions**:
    - The simulation has been initialized (agents, spaces, jurisdictions, etc have been created)
6. **Main Flow**: Running in an infinite loop, within each iteration:
    - call the `update` method on each agent
    - call the `update` method on each space
7. **Alternative Flow 1**: If a `quit` command is received:
    - exit out of main simulation loop
8. **Alternative Flow 2**: If a `pause` or `resume` command is received:
    - toggle the simulation pause state
9. **Alternative Flow 3**: If any other command is received:
    - process command and apply side-effects
10. **Post Condition (Main Flow)**:
    - stay in main flow
11. **Post Condition (Alternative Flow 2)**:
    - while the simulation is paused, stay away from the main flow
    - else go back to main flow
12. **Post Condition (Alternative Flow 3)**:
    - go back to main flow

### Tests

1. Test quit command
    - Start a simulation
    - Send a quit command to the simulation's command channel
    - If the simulation does not return from its loop, FAIL
2. Test pause command
    - Start a simulation
    - Send a pause command to the simulation's command channel
    - If the simulation does not enter a paused state, FAIL
    - If the simulation enters the main flow while it is in th paused state, FAIL
3. Test arbitrary command
    - Start a simulation
    - Send any arbitrary command to the simulation's command channel
    - Assert that the expected side-effects have been applied to the simulation

## D2 (v1)

1. **Title**: Agent update subroutine
2. **Purpose**: To simulate the infection state transition and movement of an agent within a single timestep of the simulation
3. **Associated User Stories**:
4. **Associated Use Cases**: D1 (v1), D3 (v1)
5. **Actors**: Simulation Engine
6. **Preconditions**:
    - The main simulation loop is running
7. **Main Flow**:
    - if agent is in the `Dead` state, return
    - call the `updateState` method
    - call the `updateLocation` method
8. **Post Condition**:
    - the agent's state has potentially been updated
    - the agent's location has potentially been updated

### Tests

1. Perform tests for D3
2. Perform tests for D4

## D3 (v1)

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

### Tests

1. Test that agent state updates correctly

    - initialize agent in a known state with a known transition duration
    - call agent state update with mock simulator instance, each time advancing the epoch until known duration is reached
    - assert that agent state transitioned to new expected state
    - repeat above for every possible state transition

## D4 (v1)

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

### Tests

1. Test that agent location updates correctly

    - initialize agent in a known location with a known next_move_epoch
    - call agent state update with mock simulator instance, each time advancing the epoch until known next_move_epoch is reached
    - assert that agent location transitioned to new expected location (this is not deterministic, as next location is determined randomly, but maybe can be tested using a seeded RNG)

## D5 (v1)

1. **Title**: Space update subroutine
2. **Purpose**: To simulate the change in state of a space within a single timestep of the simulation
3. **Associated User Stories**:
4. **Associated Use Cases**: D1 (v1)
5. **Actors**: Simulation Engine
6. **Preconditions**:
    - The main simulation loop is running
7. **Main Flow**:
    - for each infectious agent in the space, increment infectious quanta in the space according to a discretized version of the Wells-Riley model
    - decrement infectious quanta due to ventillation, based on the ventillation rate of the space
8. **Post Condition**:
    - the space's infectious quanta is updated

### Tests

1. Test correctness of discretized Wells-Riley model

    - introduce an infectious agent with a known pulmmonary ventilation rate and quanta emission rate into a space with a known volume and ventillation rate
    - simulate some time steps such that the elapsed duration > 0, then record the amount of infectious quanta in the space
    - calculate the expected infectious quanta analytically for the elapsed duration
    - assert that the difference between the expected and measured infectious quanta is within some epsilon > 0
