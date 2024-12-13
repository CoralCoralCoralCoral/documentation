# Use Cases

### 10 (v1) [User story 5 v2]

**Title:** Oracle Giving Suggestions for Intervention

**Purpose:** The Oracle should give advice upon meeting certain thresholds.

**Associated User Stories:** User story 5 (v2) 

**Actors:** 
- User
- Oracle  

**Preconditions:** A set limit has been reached.

**Main Flow:** Regular flow of activities.

- **Step 1** - The Oracle pops up and pauses the game.  

- **Step 2** - The Oracle informs the user of the problem (e.g., hospitals nearing full capacity) and highlights the urgency of handling the situation.  

- **Step 3** - The Oracle gives advice on potential interventions to solve the issue. The user can ask for additional advice. Go to the Alternative Flow.  

- **Step 4** - The user dismisses the Oracle and continues playing.  

**Alternative Flow:** Exceptions to main flow.

- **Step 1** - The Oracle explains why the intervention could help. The user can ask for alternative actions to take.  

- **Step 2** - Other actions are suggested to the user.  

- **Step 3** - The user dismisses the Oracle and continues playing.  

**Postcondition:** The game is paused, and the user can resume playing at any time.

**Test:**
- **Step 1** - Start game and make sure that the game is in a state that would require the oracle to pop up.
- **Step 2** - Check to see if oracle pops up when preconditions limit is met. If not FAIL.
- **Step 3** - Dismiss the oracle and restart the game. Check to see if game restarts correctly. If not FAIL.

---

### 11 (v1) [User story 5 v2]

**Title:** Oracle Giving Suggestions for Surveillance

**Purpose:** The Oracle should give advice upon meeting certain thresholds.

**Associated User Stories:** User story 5 (v2) 

**Actors:** 
- User
- Oracle  

**Preconditions:** The difference between real data and visible data has reached a certain threshold.

**Main Flow:** Regular flow of activities.

- **Step 1** - The Oracle pops up and pauses the game.  

- **Step 2** - The Oracle informs the user of the problem (e.g., poor testing in a jurisdiction leading to inaccurate data on the epidemic’s spread) and highlights the urgency of addressing the situation.  

- **Step 3** - The Oracle advises the user to consider increasing testing or employing a different testing method to resolve the issue. The user can request additional advice. Go to the Alternative Flow.  

- **Step 4** - The user dismisses the Oracle and continues playing.  

**Alternative Flow:** Exceptions to main flow.

- **Step 1** - The Oracle explains why testing is important. The user can request alternative actions to take.  

- **Step 2** - Other actions are suggested to the user.  

- **Step 3** - The user dismisses the Oracle and continues playing.  


**Postcondition:** The game is paused, and the user can resume playing at any time.

 **Test:**
- **Step 1** -  Start game and make sure that the game is in a state that would require the oracle to pop up.
- **Step 2** - Check to see if oracle pops up when preconditions limit is met. If not FAIL.
- **Step 3** - Dismiss the oracle and restart the game. Check to see if game restarts correctly. If not FAIL.

---

### 12 (v1) [User story 5 v2]

**Title:** Oracle Giving Suggestions for Research

**Purpose:** The Oracle should give advice upon meeting certain thresholds.

**Associated User Stories:** User story 5 (v2)  

**Actors:** 
- User 
- Oracle  

**Preconditions:** A set amount of time or number of deaths has been reached without the user initiating a research project.

**Main Flow:** Regular flow of activities.

- **Step 1** - The Oracle pops up and pauses the game.  

- **Step 2** - The Oracle informs the user of the problem, indicating that they have not started a new research project in a specified time frame.  

- **Step 3** - The Oracle advises the user to consider starting an appropriate research project. The user can request additional advice. Go to Alternative Flow.  

- **Step 4** - The user dismisses the Oracle and continues playing.  

**Alternative Flow:** Exceptions to main flow.

- **Step 1** - The Oracle explains the benefits of research and how it can help in controlling the disease. The user can request alternative actions to take.  

- **Step 2** - Other actions are suggested to the user.  

- **Step 3** - The user dismisses the Oracle and continues playing.  


**Postcondition:** The game is paused, and the user can resume playing at any time.

**Test:** 
- **Step 1** - Start game and make sure that the game is in a state that would require the oracle to pop up.
- **Step 2** - Check to see if oracle pops up when preconditions limit is met. If not FAIL.
- **Step 3** - Dismiss the oracle and restart the game. Check to see if game restarts correctly. If not FAIL.

---

### 13 (v1) [User story 13 v1]

**Title:** Surveillance Actions in Healthcare Spaces

**Purpose:** The user should be able to take action to increase their surveillance so that they can obtain better data.

**Associated User Stories:** User story 13 (v1)  

**Actors:** User  

**Preconditions:** The user has selected the jurisdiction and the surveillance actions.

**Main Flow:** Regular flow of activities.

- **Step 1** - The game displays the actions the user can take.  

- **Step 2** - The User will select one of the surveillance actions that are currently available. If the user wants to select an action they have not unlocked then go to alternative flow 1.

- **Step 3** - The user enables the selected action.  

- **Step 4** - The user continues playing.  

**Alternative Flow:** Exceptions to main flow.

- **Step 1** - The user hovers over the locked action.  

- **Step 2** - Information about the action and instructions on how to unlock it appear underneath the action.  

- **Step 3** - The user continues playing.  

**Postcondition:** The action is applied, and a pop-up informs the user of the change.

**Test:**
- **Step 1** - Select the testing strategy button.
- **Step 2** - Select a different testing strategy. Check if it is implemented correctly. If not FAIL.
