### 19 (v1) [User story 20 v1]

**Title:** GDP System  

**Purpose:** Model GDP by the behavior of agents.  

**Associated User Stories:** 20 (v1)  

**Actors:** 
- System 
- User  

**Preconditions:** The game is running correctly.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - An agent spends time at an office.  
- **Step 2** - GDP is generated based on the amount of time times the productivity of the agents. Productivity is based on UK average data.  
- **Step 3** - GDP is generated when agents spend time in social spaces.  
- **Step 4** - The User initiates a lockdown.  
- **Step 5** - Agents cannot spend time in offices and social spaces, so GDP decreases.  

**Alternative Flow #1:** Exceptions to main flow.  

**Postcondition:** The game will continue to play.  

**Tests:**  
- **Test 1:**  
  - **Step 1** - Run the game, check that the GDP generated is the number expected. If not, FAIL.  
  - **Step 2** - Implement a lockdown. Check that GDP drops by the correct amount. If not, FAIL.  

---

### 20 (v1) [User story 21 v1]

**Title:** Influence Actions  

**Purpose:** Implement actions in order to increase agents' compliance.  

**Associated User Stories:** 21 (v1)  

**Actors:**
- User
- System  

**Preconditions:** The User navigates to the influence actions tab.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The User selects the influence action they want to implement. If the User does not have enough resources, go to Alternative Flow 1.  
- **Step 2** - The System increases the compliance of agents based on the action taken.  
- **Step 3** - The simulation updates, and the User can continue playing.  

**Alternative Flow #1:** Exceptions to main flow.  
- **Step 1** - The System sends an error message informing the User that they cannot do this action due to insufficient resources.  

**Postconditions:** The game continues to play with the updated compliance and resources.  

**Test:**  
  - **Step 1** - Select an influence action that cannot be afforded. If the action is allowed and no error message is sent, FAIL.  
  - **Step 2** - Select an influence action that can be afforded. Check using dev tools that:  
    - Resources are deducted correctly. If not, FAIL.  
    - Compliance is increased correctly. If not, FAIL.  

---

### 21 (v1) [User story 22 v1]

**Title:** Play as Different Countries  

**Purpose:** Allow the User to play as different countries.  

**Associated User Stories:** 22 (v1)  

**Actors:** User  

**Preconditions:** The game has the capability to play as different countries.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The User selects to play as a different country at the main menu.  
- **Step 2** - The User can select from a list of available countries to play as.  
- **Step 3** - After selecting their chosen country, the User starts the game.  

**Alternative Flow:** Exceptions to main flow.  

**Postcondition:** The game begins in the User's chosen country.  

**Test:**  Select a country to play as and start the game. If the game does not start as the chosen country correctly, FAIL.  

---

### 22 (v1) [User story 23 v1]

**Title:** Different Diseases  

**Purpose:** Allow the User to learn different strategies for different diseases.  

**Associated User Stories:** 23 (v1)  

**Actors:** User  

**Preconditions:** The User has navigated to the main menu.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The User selects the start options and navigates to diseases.  
- **Step 2** - The User inputs the disease attributes they want to play against. Alternative flow.  
- **Step 3** - The User can start the game with their chosen disease.  

**Alternative Flow:** Exceptions to main flow.  
- **Exception 1** - The User selects a random disease, and the disease attributes are randomized.  

**Postcondition:** The game successfully starts with the chosen disease.  

**Test:** 
  - **Step 1** - Select a different disease at the main menu.  
  - **Step 2** - Start the game and check that the disease running matches the disease chosen. If not, FAIL.  
