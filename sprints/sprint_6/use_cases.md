# Use Cases

## 19 (v1) [[User story 20 v1]](user_stories.md) 
### 1. Title -- GDP System 

### 2. Purpose -- Model GDP by the behaviour of agents

### 3. Associated User Stories -- 20 (v1)

### 4. Actors -- The System, the User

### 5. Preconditions -- The game is running correctly.

### 6. Main Flow -- regular flow of activities

#### Step 1 - An agents spends time at an office.

#### Step 2 - GDP is generated based on the amount of time times the productivity of the agents. Productivity is based on UK average data.

#### Step 3 - GDP is generated when agents spend time in social spaces.

#### Step 4 - The User intiates a lockdown.

#### Step 5 - Agents cannot spend time in offices and socail spaces so GDP decreases.

### 7. Alternative Flow #1 -- exceptions to main flow

### 8. Postcondition -- The game will continue to play.

### 9. Tests

#### Test 1
- Step 1: Run the game, check that the GDP generated is the number expected. If not FAIL.
- Step 2: Implement a lockdown. Check that GDP drops by the correct amount. If not FAIL.



## 20 (v1) [[User story 21 v1]](user_stories.md)

### 1. Title -- Influence Actions

### 2. Purpose -- Implement actions in order to increase agents compliance.

### 3. Associated User Stories -- 21 (v1)

### 4. Actors -- The User, the System

### 5. Preconditions -- The User navigates to the influence actions tab.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The User selects the influence action they want to implement. If the User does not have enough resources go to Alternative Flow 1

#### Step 2 - The System increases the compliance of agents based on the action taken.

#### Step 3 - The simulation updates and the User can continue playing.

### 7. Alternative Flow 1 -- exceptions to main flow

#### Step 1 - The System sends an error message informing the User that they cannot do this action due to insufficient resources.

### 8. Postconditions - The game continues to play with the updated compliance and resources.

### Tests

#### Test 1
- Step 1: Select an influence action that cannot be afforded. If action is allowed and no error message is sent FAIL.
- Step 2: Select an influence action that can be afforded. Check using dev tools that:
  - Resources are deducted correctly. If nt FAIL.
  - Compliance is increases correctly. If not FAIL. 



## 21 (v1) [[User story 22 v1]](user_stories.md)

### 1. Title -- Play as Different Countries  

### 2. Purpose --  Allow the User to play as different countries

### 3. Associated User Stories -- 22 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The game has the capability to play as different countries.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The User selecs to play as a different countries at the main menu.

#### Step 2 - The User can select from a list of available countries to play as.

#### Step 3 - After selecting their chosen country, the User starts the game.

### 7. Alternative Flow -- exceptions to main flow

### 8. Postcondition -- The game begins in the User chosen country

### 9. Tests

#### Test 1
- Step 1: Select a country to play as and start the game. If game does not start as chosen country correctly FAIL.



## 22 (v1) [[User story 23 v1]](user_stories.md)

### 1. Title -- Different Diseases 

### 2. Purpose -- So that the User can learn different startgies for different diseases.

### 3. Associated User Stories -- 23 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The User has navigated to the main menu.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The User selects the start options and navigates to diseases.

#### Step 2 - The User inputs the disease attributes that the want to play against. Alternative flow.

#### Step 3 - The user can start the game with their chosen disease.

### 7. Alternative Flow -- exceptions to main flow

#### Exception 1 - The User selects random disease and the disease attributes are randomized.

### 8. Postcondition -- The game successfully starts with the chosen disease.

### 9. Tests

#### Test 1
- Step 1: Select a different disease at main menu.  
- Step 2: Start the game and check that disease runing matches the disease chosen. If not FAIL.
