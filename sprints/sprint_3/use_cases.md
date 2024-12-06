# Use Cases

## 1 (v1)

### 1. Title -- Pause and Resume the Game

### 2. Purpose -- As a user, I want to pause and resume the game so that I can take breaks to strategize and think.

### 3. Associated User Stories -- 8 (v1)

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

## 2 (v1)

### 1. Title -- Map modes

### 2. Purpose -- As a user, I want to be able to apply different map modes so that I can .

### 3. Associated User Stories -- 10 (v1)

### 4. Actors -- The User.

### 5. Preconditions -- The user press a button to see a different map mode.

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user can select from a list of different options for which data they want to see visualized on the map.

#### Step 2 - The user presses on one of them and the game will change what data is visualized on the map,

#### Step 3 - The UI map will change to show the needed data and the user can continue playing the game

### 7. Alternative Flow -- exceptions to main flow

### 8. Postcondition -- The game successfully shows the updated map.

### 8. Tests - Does the map update when the button has been pressed by the player?
