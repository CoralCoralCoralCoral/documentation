# Use Cases

### 14 (v1) [[User story 15 v1]](../sprint_4/user_stories.md) [[User story 12 v1]](../sprint_3/user_stories.md)

**Title:** Accuracy Changes by Area

**Purpose:** As a public health official, I want to know how testing accuracy varies by area so I can allocate resources more effectively.

**Associated User Stories:** 15 (v1), 12 (v1) 

**Actors:** User  

**Preconditions:** The game is running correctly.

**Main Flow:** Regular flow of activities.

- **Step 1** - The user selects a specific area on the map.  

- **Step 2** - The system displays the testing accuracy in that area (e.g., false positive and negative rates).  

- **Step 3** - The user decides whether to change the testing method or improve existing strategies. Go to Alternative Flow 1.  

- **Step 4** - The system updates and shows the rates of infection and other important statistics.  

**Alternative Flow 1:** Exceptions to main flow.

- **Step 1** - The UI shows all available and unavailable testing methods, as well as the testing method(s) currently in use.  

- **Step 2** - The user selects one of the available testing methods to implement or spends more on improving the current method. If the user tries to select an unavailable method, go to Alternative Flow 2.  

- **Step 3** - The system updates and shows the effects of the changes.  

**Alternative Flow 2:** Exceptions to main flow.

- **Step 1** - After clicking a locked testing method, the user is informed of how to unlock it and its benefits, displayed below.  

- **Step 2** - The user continues playing the game.  

**Postcondition:** The game continues after the user completes their changes, which are implemented by the system.

**Test:**
- **Step 1:** Select a specific jurisdiction. Check to see if metrics shown are from that jurisdiction chosen. If not FAIL.
- **Step 2:** Increase testing investment. Check if this has the correct impact on test metrics shown. If not FAIL.

---

### 15 (v1) [[User story 14 v1]](../sprint_4/user_stories.md)

**Title:** Prioritize Testing for High-Risk Groups  

**Purpose:** High-risk groups are identified based on available data (e.g. elderly or those with pre-existing conditions). Actions are taken to help them.  

**Associated User Stories:** 14 (v1)  

**Actors:** User  

**Preconditions:** The game is running correctly.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The player selects high-risk groups for testing.  
- **Step 2** - The system allocates resources to prioritize these groups.  
- **Step 3** - The simulation updates to show testing results for high-risk populations.  

**Alternative Flow:** Exceptions to main flow.  

**Postconditions:**  
- **Postcondition 1** - High-risk groups are tested, influencing the progression of the epidemic in the simulation.  
- **Postcondition 2** - If prioritization delays testing for others, the system provides a warning.  

**Test:**  
- **Step 1** - Select a specific jurisdiction. Check to see if metrics shown are from that jurisdiction chosen. If not, FAIL.  
- **Step 2** - Increase testing investment. Check if this has the correct impact on test metrics shown. If not, FAIL.  

---

### 16 (v1) [[User story 16 v1]](user_stories.md)

**Title:** See How Delayed Testing Affects the Outbreak  

**Purpose:** As a public health official, I want to understand how delays in testing affect the spread of the disease so I can make better plans to reduce these delays.  

**Associated User Stories:** 16 (v1)  

**Actors:** The User  

**Preconditions:** The game is running correctly.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The user deploys a testing strategy and sets its start date.  
- **Step 2** - The system calculates delays based on available resources and logistics.  
- **Step 3** - The simulation shows how delays impact infection rates and the epidemic’s spread.  
- **Step 4** - The player adjusts interventions (e.g., adding more labs or improving logistics) to reduce delays.  

**Alternative Flow:** Exceptions to main flow.  

**Postcondition:** The simulation reflects the real-world consequences of delays, allowing the player to refine their plans.  

**Test:**  
- **Step 1** - Select a specific jurisdiction. Check to see if metrics shown are from that jurisdiction chosen. If not, FAIL.  
- **Step 2** - Increase testing investment. Check if this has the correct impact on test metrics shown. If not, FAIL.  

---

### 17 (v1) [[User story 10 v2]](user_stories.md)

**Title:** Save Games  

**Purpose:** As a user, I want to save my game so that I can stop playing and come back later.  

**Associated User Stories:** 10 (v2)  

**Actors:** The User  

**Preconditions:** The game has a functioning save system.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The user goes to the main menu and presses the save button.  
- **Step 2** - The system generates a JSON file with relevant data and sends this to the user. If the message fails, go to the alternative flow.  
- **Step 3** - The user can download the save file and continue playing.  

**Alternative Flow:** Exceptions to main flow.

**Exception:** Error message is sent to the user or system that the save file has not been sent.  

**Postcondition:** The game successfully runs.  

**Test:**  
- **Step 1** - Press the save game button. Check to see if save file is received. If not, FAIL.  
- **Step 2** - Start game using received save file. Check to see if the game continues from where you left off. If not, FAIL.  

---

### 18 (v1) [[User story 19 v1]](user_stories.md)

**Title:** Load Games  

**Purpose:** As a user, I want to save and load my save so that I can stop playing and come back later.  

**Associated User Stories:** 19 (v1)  

**Actors:** User  

**Preconditions:** The user goes to the main webpage of the game.  

**Main Flow:** Regular flow of activities.  
- **Step 1** - The user presses the load game button on the main menu page.  
- **Step 2** - The user selects a file to upload as their save. If the save file is invalid, go to the alternative flow.  
- **Step 3** - The user can start playing the game from the game state found in the save.  

**Alternative Flow:** Exceptions to main flow.  

**Exception:**  Error message is sent to the user or system that the save file is not valid.  

**Postcondition:** The game successfully runs from the point of the save.  

**Test:** Start game using received save file. Check to see if the game continues from where you left off. If not, FAIL.  

