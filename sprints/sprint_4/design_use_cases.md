# Design Use Cases

## D12 (v1)

1. **Title**: Healthcare Space Surveillance
2. **Purpose**: To simulate infectious disease surveillance in healthcare spaces
3. **Associated User Stories**:
4. **Associated Use Cases**: D11
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

## D13 (v1)

1. **Title**: Emulation of Test Backlog in Healthcare Spaces
2. **Purpose**: To emulate a test backlog when a healthcare space's test capacity has been reached
3. **Associated User Stories**:
4. **Associated Use Cases**: D10
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
