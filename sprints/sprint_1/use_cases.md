# Use Cases

### 1 (v1) [[User story 1 v1]](user_stories.md)
**Title:** UI

**Purpose:** Have a good visualisation of the information for the user.

**Associated User Stories:** 1 (v1)

**Actors:** 
- User
- System

**Preconditions:** The system has a functional simulation engine ready to display data. 

**Main Flow:** regular flow of activities.

 - **Step 1** - The user opens the webpage.

 - **Step 2** - The system has a functional simulation engine ready to display data with these key functions: 
    - A map showing affected areas. 
    - Graphs showing infection trends. 
    - A panel with simulation controls (e.g start, pause, reset). 

- **Step 3** - The user observes how data changes over time. 

**Alternative Flow:** Exceptions to main flow.

**Exception:** If the user interface fails to load, the system displays an error message and provides troubleshooting steps. 

**Postcondition:** The user has access to an intuitive and visually appealing interface to monitor the simulation. 



### 2 (v1) [[User story 2 v1]](user_stories.md)

**Title:** Enable Interactive Gameplay 

**Purpose:** The system provides interactive elements like buttons, sliders and clickable maps. 

**Associated User Stories:** 2 (v1)

**Actors:**
- User
- System

**Preconditions:** The system has a functional simulation engine and UI. 

**Main Flow:** Regular flow of activities.

**Step 1** - The user selects options from the interface (e.g. deploying a strategy, adjusting parameters). 

**Step 2** - The system responds immediately to user input, updating the simulation in real-time.  

**Step 3** - The user receives feedback on their actions (e.g. changes in infection rates or resource allocation). 

**Alternative Flow:** Exceptions to main flow.

**Exception:** If input is invalid (e.g. exceeding resource limits), the system displays a warning and suggests corrections. 

**Postcondition:** The user can seamlessly interact with the game to influence the simulation. 



## 3 (v1) [[User story 3 v1]](user_stories.md)

**Title:** Simulate Epidemic Scenarios 

**Purpose:** The system provides a range of epidemic scenarios with adjustable parameters (e.g., infection rate, population density). 

**Associated User Stories:** 3 (v1)

**Actors:** 
- User 
- System

**Preconditions:** The simulation engine is functional and ready to execute scenarios. 

**Main Flow:** Regular flow of activities

**Step 1** - The user selects or customizes an epidemic scenario (e.g., a new virus, a specific region). 

**Step 2** - The system runs the simulation, showing the spread of the disease over time. 

**Step 3** - The user can pause mid-simulation and rewind post-simulation to explore different outcomes. 

**Alternative Flow:**  Exceptions to main flow.

**Exceptions:**
- If the selected scenario has errors (e.g., conflicting parameters), the system prompts the user to adjust settings.
- If the simulation engine encounters issues, the system provides debug options or loads a default scenario. 

**Postcondition:** The simulation runs functionally.



### 4 (v1) [[User story 4 v1]](user_stories.md)

**Title:** Use Multiple Strategies for Realistic Gameplay

**Purpose:** As a user, I want to use multiple strategies so that the gameplay is diverse and realistic. 

**Associated User Stories:** 4 (v1)

**Actors:**
- User
- System

**Preconditions:** 
- The system supports a variety of strategies (e.g., lockdowns, mass testing, vaccination campaigns).
- Each strategy has defined effects and outcomes in the simulation. 

**Main Flow:** Regular flow of activities.

**Step 1** - The user chooses a strategy from a list or combination of strategies. 

**Step 2** - The system simulates the impact of the chosen strategies, showing how they affect infection rates and resource usage. The system runs the simulation, showing the spread of the disease over time. 

**Step 3** - The user evaluates outcomes and decides whether to adjust or add new strategies. 

**Alternative Flow:** Exceptions to main flow.

**Exceptions:**
- If a strategy is unavailable due to resource limitations, the system suggests alternatives. 
- If conflicting strategies are chosen (e.g., simultaneous lockdown and mass gatherings), the system provides a warning and requests clarification. 

**Postcondition:** The user experiences diverse gameplay with realistic outcomes based on strategic decisions. 
