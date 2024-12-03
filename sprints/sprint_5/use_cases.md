
# Use Cases

## 1 (v1)

### 1. Title -- Accuracy Changes by Area 

### 2. Purpose --  As a public health official, I want to know how testing accuracy varies by area so I can allocate resources more effectively.   

### 3. Associated User Stories -- 14 (v1), 11 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The game is running correctly.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The User selects a specific area on the map.  

#### Step 2 - The system displays the testing accuracy in that area (e.g., false positive and negative rates).

#### Step 3 - The User decides whether to change the testing method or improve existing strategies. Go to alternative flow 1.  

#### Step 4 - The system updates and shows the rates of infection and other improtant statistics.  

### 7. Alternative Flow #1 -- exceptions to main flow

#### Step 1 - The UI will show all available and unavailable testing methods, as well as which testing method/s are currently being used.

#### Step 2 - The user can select one of the available testing methods to implement or to spend more on a current method. If the user tries to select an unavalibale method go to alternative flow 2.

#### Step 3 - The system updates and shows the effects of the changes. 

### 7. Alternative Flow #2 -- exceptions to main flow

#### Step 1 - After the user clicks the locked testing method they will be told how they can unlock it and it's benefits bellow.

#### Step 2 - The user continues playing the game.

### 8. Postcondition -- The game will continue to play after the user is finished. Any changes made by the user are done by the system.


## 2 (v1)

### 1. Title -- Prioritize Testing for High-Risk Groups  

### 2. Purpose --  High-risk groups are identified based on available data (e.g., elderly or those with pre-existing conditions). Actions are taken to help them. 

### 3. Associated User Stories -- 13 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The game is running correctly.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The player selects high-risk groups for testing.    

#### Step 2 - The system allocates resources to prioritize these groups. 

#### Step 3 - The simulation updates to show testing results for high-risk populations.   

### 7. Alternative Flow #1 -- exceptions to main flow

#### Step 1 - If prioritization delays testing for others, the system provides a warning. 

### 8. Postcondition -- High-risk groups are tested, influencing the progression of the epidemic in the simulation. 


## 3 (v1)

### 1. Title -- See How Delayed Testing Affects the Outbreak    

### 2. Purpose --   As a public health official, I want to understand how delays in testing affect the spread of the disease so I can make better plans to reduce these delays

### 3. Associated User Stories -- 15 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The game is running correctly.

### 6. Main Flow -- regular flow of activities

#### Step 1 - the user deploys a testing strategy and sets its start date.     

#### Step 2 - The system calculates delays based on available resources and logistics

#### Step 3 - The simulation shows how delays impact infection rates and the epidemic’s spread. 

#### Step 4 - The player adjusts interventions (e.g., adding more labs or improving logistics) to reduce delays. 

### 7. Alternative Flow #1 -- exceptions to main flow

#### Step 1 - The player can choose alternative strategies to compensate for delays.   

### 8. Postcondition --   The simulation reflects the real-world consequences of delays, allowing the player to refine their plans.   

