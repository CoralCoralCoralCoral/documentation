# Use Cases

### 8 (v1) [[User story 9 v1]](user_stories.md)

**Title:** Pause and Resume the Game

**Purpose:** As a user, I want to pause and resume the game so that I can take breaks to strategize and think.

**Associated User Stories:** 9 (v1)
  
**Actors:** User  

**Preconditions:** The game has a functioning simulation engine with adjustable flow controls. A visible pause/resume button or shortcut is available in the user interface.

**Main Flow:** Regular flow of activities.

- **Step 1** - The user presses the pause button or triggers a pause command.  

- **Step 2** - The system halts all simulation activity, freezing the current state. If this fails, go to the alternative flow.  

- **Step 3** - The user can interact with the game to see data and plan to initiate actions.  

- **Step 4** - The user resumes the game by pressing the resume button or triggering the corresponding command. If this fails, go to the alternative flow.  

- **Step 5** - The system restarts the simulation, continuing from the paused state.  

**Alternative Flow:** Exceptions to main flow.

**Exception:** An error message is sent to the user indicating that the pause/play function is not working correctly.  

**Postcondition:** The game successfully resumes with any changes made during the pause implemented.



### 9 (v1) [[User story 11 v1]](user_stories.md)

**Title:** Metrics Graphs

**Purpose:** As a user, I want to be able to see a specific metrics plot for a given jurisdiction.

**Associated User Stories:** 11 (v1)  

**Actors:** System, User  

**Preconditions:** A jurisdiction is selected. [Reference Use Case 5 (v1)](../sprint_2/use_cases.md)

**Main Flow:** Regular flow of activities.

- **Step 1** - User selects a metric to view.  

- **Step 2** - System retrieves the data for the specified metrics for the selected jurisdiction.  

- **Step 3** - The system constructs a plot for the retrieved data and displays it in the user interface.  

**Alternative Flow:** None specified.

**Postcondition:** The game continues playing.

**Tests:** Does the map update when the button has been pressed by the player?
