# Design Use Cases

## D10 (v1) [[User Story 13 (v1)]](../sprint_4/use_cases.md)

1. **Title**: Healthcare Space Surveillance
2. **Purpose**: To simulate infectious disease surveillance in healthcare spaces
3. **Associated User Stories**: 13 (v1)
4. **Associated Use Cases**: D11 (v1)
5. **Actors**: Simulation Engine, Healthcare Space
6. **Preconditions**:
    - The simulation is running
7. **Main Flow**: test strategy is `TestSymptomatic`
    - when an infected and symptomatic agent enters the space, sample a positive test using a Bernoulli distribution where the probability is set to the test sensitivity
    - when a symptomatic (but uninfected) agent enters the space, sample a negative test using a Bernoulli distribution where the probability is set to the test specificity
    - add test result to a results queue
8. **Alternative Flow 1**: test strategy is `TestEveryone`
    - when an infected agent enters the space, sample a positive test using a Bernoulli distribution where the probability is set to the test sensitivity
    - for everyone else, sample a negative test using a Bernoulli distribution where the probability is set to the test specificity
    - add test result to a results queue
9. **Alternative Flow 2**: test strategy is `TestNone`
    - do not simulate testing when agents enter the space
10. **Post Condition**:
    - test results have been added to a queue

### Tests

1. Test that tests are conducted correctly based on the state of agents entering healthcare spaces

    - create a healthcare space with a known `TestStrategy`
    - create an agent with a known infection state
    - add agent to healthcare space
    - evaluate expected test result using seeded rng with determinism
    - progress healthcare space state using mock simulation
    - read back test result from healthcare space's test queue
    - assert that test result read from queue is equal to expected test result
    - repeat test for different combinations of agent state and `TestStrategy`

## D11 (v1) [[User Story 13 (v1)]](../sprint_4/use_cases.md) [[User Story 16 (v1)]](../sprint_5/use_cases.md)

1. **Title**: Emulation of Test Backlog in Healthcare Spaces
2. **Purpose**: To emulate a test backlog when a healthcare space's test capacity has been reached
3. **Associated User Stories**: 13 (v1), 14 (v1)
4. **Associated Use Cases**: D10 (v1)
5. **Actors**: Simulation Engine, Healthcare Space
6. **Preconditions**:
    - The simulation is running
    - it is the last epoch of the (in-game) day (it is the end of the in-game day)
7. **Main Flow**:
    - start removing the oldest test results from the queue (from the head of the queue) up to the healthcare space's daily `test_capacity`
    - aggregate the results of these tests (positives and negatives)
    - dispatch a `TestingUpdate` event that contains the aggregate test results as well as the number of tests that remain in the queue (test backlog)
8. **Post Condition**:
    - test results have been removed from the queue

### Tests

1. Test that tests are being cleared from healthcare space's test backlog
    - create a healthcare space with `TestStrategy` set to `test_everyone`
    - create several agents where number of agents is some known number > healthcare space's daily test capacity
    - add agents to healthcare space
    - assert that healthcare space's backlog has grown by number of agents
    - progress healthcare space state using mock simulation all the way to the end of the in-game day
    - assert that new size of healthcare space's backlog is exactly equal to the difference between the number of afents and the healthcare space's daily test capacity
