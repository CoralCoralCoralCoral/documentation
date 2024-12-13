# Use Cases

## 1 (v1) [[User story 1 v1]](user_stories.md)

### 1. Title -- UI

### 2. Purpose -- Have a good visualisation of the information for the user.

### 3. Associated User Stories -- 1 (v1)

### 4. Actors -- The User and the System

### 5. Preconditions -- The system has a functional simulation engine ready to display data. 

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user opens the webpage.

#### Step 2 - The system has a functional simulation engine ready to display data with these key functions: 

- A map showing affected areas. 
- Graphs showing infection trends. 
- A panel with simulation controls (start, pause, reset). 

#### Step 3 - The user observes how data changes over time. 

### 7. Alternative Flow -- exceptions to main flow

#### Exception - If the user interface fails to load, the system displays an error message and provides troubleshooting steps. 

### 8. Postcondition -- The user has access to an intuitive and visually appealing interface to monitor the simulation. 

### 9. Tests

#### Test 1 (Start game UI)
- Step 1: In the test suite navigate to the start up screen of the game. If start up screen does not load FAIL.
- Step 2: Check if there is a button to start the game. If button does not exist FAIL.

#### Test 2 (In-game UI)
- Step 1: Check if the map has loaded. If not FAIL.
- Step 2: Check if graphs have loaded. If not FAIL.
- Step 3: Check if contral panel has loaded. If not FAIL.

#### Test 3 (In-game UI Updates)
- Step 1: Check if the UI is connected to a simulation instance. If not FAIL.
- Step 2: Check if the UI recieves data from simulation instance at the expected frequency (demermined while running test). If not FAIL.
- Step 3: Check if UI displays the game state changes. If not FAIL.


## 2 (v1) [[User story 2 v1]](user_stories.md)

### 1. Title -- Enable Interactive Gameplay 

### 2. Purpose -- The system provides interactive elements like buttons, sliders, and clickable maps. 

### 3. Associated User Stories -- 2 (v1)

### 4. Actors -- The User and the System

### 5. Preconditions -- The system has a functional simulation engine and UI. 

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user selects options from the interface (e.g., deploying a strategy, adjusting parameters). 

#### Step 2 - The system responds immediately to user input, updating the simulation in real-time.  

#### Step 3 - The user receives feedback on their actions (e.g., changes in infection rates or resource allocation). 

### 7. Alternative Flow -- exceptions to main flow

#### Exception - If input is invalid (e.g., exceeding resource limits), the system displays a warning and suggests corrections. 

### 8. Postcondition -- The user can seamlessly interact with the game to influence the simulation. 

### 9. Tests

#### Test 1 (UI interaction)
- Step 1: For each interaction:
  - dispatch interaction when the action would be deemed invalid. If UI does not reject with an "invalid action" message FAIL.
  - dispatch interaction when the action would be deemed valid. If UI does not accept the action FAIL.
    - The UI sends a command message to the API server. If the message fails to be sent FAIL.



## 3 (v1) [[User story 3 v1]](user_stories.md)

### 1. Title -- Simulate Epidemic Scenarios 

### 2. Purpose -- The system provides a range of epidemic scenarios with adjustable parameters (e.g., infection rate, population density). 

### 3. Associated User Stories -- 3 (v1)

### 4. Actors -- The User and the System

### 5. Preconditions -- The simulation engine is functional and ready to execute scenarios. 

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user selects or customizes an epidemic scenario (e.g., a new virus, a specific region). 

#### Step 2 - The system runs the simulation, showing the spread of the disease over time. 

#### Step 3 - The user can pause mid-simulation and restart to take time to think and plan. 

### 7. Alternative Flow -- exceptions to main flow

#### Exception 1 - If the selected scenario has errors (e.g., conflicting parameters), the system prompts the user to adjust settings.

#### Exception 2 - If the simulation engine encounters issues, the system provides debug options or loads a default scenario. 

### 8. Postcondition -- The simulation run functionally.

### 9. Tests

#### Test 1 (Simulation functionality)
- Step 1: Initalize the simulation. If the simulations does not start FAIL.
- Step 2: Let the simulation run. Check if virus successfully spread in realistic manner with no intervention. If not FAIL.
- Step 3: Pause the simulation. Check if simulation successfully pauses. If not FAIL.
- Step 4: Restart the simulation. Check if simulation successfully starts. If not FAIL.




## 4 (v1) [[User story 4 v1]](user_stories.md)

### 1. Title -- Use Multiple Strategies for Realistic Gameplay

### 2. Purpose -- As a user, I want to use multiple strategies so that the gameplay is diverse and realistic. 

### 3. Associated User Stories -- 4 (v1)

### 4. Actors -- The User and the System

### 5. Preconditions -- The system supports a variety of strategies (e.g., lockdowns, mass testing, vaccination campaigns). Each strategy has defined effects and outcomes in the simulation. 

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user chooses a strategy from a list or combination of strategies. 

#### Step 2 - The system simulates the impact of the chosen strategies, showing how they affect infection rates and resource usage. The system runs the simulation, showing the spread of the disease over time. 

#### Step 3 - The user evaluates outcomes and decides whether to adjust or add new strategies. 

### 7. Alternative Flow -- exceptions to main flow

#### Exception 1 - If a strategy is unavailable due to resource limitations, the system suggests alternatives. 

#### Exception 2 - If conflicting strategies are chosen (e.g., simultaneous lockdown and mass gatherings), the system provides a warning and requests clarification. 

### 8. Postcondition -- The user experiences diverse gameplay with realistic outcomes based on strategic decisions. 

### 9. Tests

#### Test 1
- Step 1: Is there a way for a user to select a strategy (policy). If not FAIL.
- Step 2: Is that successfully implemeted by the system. If not FAIL.
- Step 3: Can you see the impact of your decision. If not FAIL.
