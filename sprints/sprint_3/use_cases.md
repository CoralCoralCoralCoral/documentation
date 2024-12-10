# Use Cases

## 8 (v1) [[User story 9 v1]](user_stories.md)

### 1. Title -- Pause and Resume the Game

### 2. Purpose -- As a user, I want to pause and resume the game so that I can take breaks to strategize and think.

### 3. Associated User Stories -- 9 (v1)

### 4. Actors -- The User.

### 5. Preconditions -- The game has a functioning simulation engine with adjustable flow controls. A visible pause/resume button or shortcut is available in the user interface.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user presses the pause button or triggers a pause command.

#### Step 2 - The system halts all simulation activity, freezing the current state. If this fails go to alternative flow 1.

#### Step 3 - The user can interact with the game to see data and plan to intiate actions.

#### Step 4 - The user resumes the game by pressing the resume button or triggering the corresponding command. If this fails go to alternative flow.

#### Step 5 - The system restarts the simulation, continuing from the paused state.

### 7. Alternative Flow -- exceptions to main flow

#### Exception 1 - Error message is sent to user that the pause/play function is not working correctly.

### 8. Postcondition -- The game successfully runs with any changes made implemented.



## 9 (v1) [[User story 11 v1]](user_stories.md)

### 1. Title -- Metrics Graphs

### 2. Purpose -- As a user, I want to be able to see a specfic metrics plot for a given jurisdiction.

### 3. Associated User Stories -- 11 (v1)

### 4. Actors -- The System, the User.

### 5. Preconditions --  A jurisdiction is selected. [Reference Use Case 5 (v1)](../sprint_2/use_cases.md)

### 6. Main Flow -- regular flow of activities

#### Step 1 - User selects a metric to view.

#### Step 2 - System retrives the data for the specified metrics for the selceted jurisdiction.

#### Step 3 - The system will contruct a plot for the retrived data and display it in the user interface.

### 7. Alternative Flow -- exceptions to main flow

### 8. Postcondition -- The game continues playing.

### 9. Tests - Does the map update when the button has been pressed by the player?
