
# Use Cases
## 5 (v1) [[User story 8 v1]](user_stories.md)

### 1. Title -- Geo Visualisation of Jurisdictions

  ### 2. Purpose -- Display the Local Authority Districts and MSOA contained within them, visualized on a map.

### 3. Associated User Stories -- 8 (v1)

### 4. Actors -- The System and the User

### 5. Preconditions -- Data for LAD and MSOA is loaded onto the UI. 

### 6. Main Flow -- regular flow of activities

#### Step 1 -  UI map shows the outlines for the LADs.

#### Step 2 - The User selects a LAD.

#### Step 3 - The System zooms into the LAD and displays the MSOAs within the LAD.

#### Step 4 - The system updates the simulation to reflect the effects of the action in the chosen area. 

### 7. Alternative Flow -- exceptions to main flow

### 8. Postcondition -- Actions are successfully applied within the specified geographic scope, optimizing resource use. 

### 9. Tests

#### Test 1
- Step 1: Check if LAD outlines are displayed on the map. If not FAIL.
- Step 2: Select LAD. Check if the currently selected LAD is the LAD that was selected. If not FAIL.
- Step 3: Check if the map state has been updated to reflect the selected LAD. If not FAIL.
  - Check if map zooms to the bounds of the selected LAD. If not FAIL.
  - Check if the outlines of the MSOAs within the LAD are displayed on the map. If not FAIL. 



## 6 (v1) [[User story 6 v1]](user_stories.md)

### 1. Title -- Implement Actions Within a Geographic Scope

### 2. Purpose -- As a user, I want to implement actions within a given geographic scope so that I can use resources efficiently

### 3. Associated User Stories -- 6 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The map displays distinct geographic regions with selectable areas. The system supports targeted actions such as testing, lockdowns, or resource distribution. 

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user selects a specific region on the map. 

#### Step 2 - The system highlights the chosen region, showing relevant data (e.g., infection rates, available resources). 

#### Step 3 - The user implements an action (e.g., deploying a testing strategy or imposing restrictions) within the selected region.

#### Step 4 - The system updates the simulation to reflect the effects of the action in the chosen area. 

### 7. Alternative Flow -- exceptions to main flow

#### Exception 1 - If the user tries to apply actions to an unselected region, the system provides a prompt to select a scope first. 

### 8. Postcondition -- Actions are successfully applied within the specified geographic scope, optimizing resource use. 



## 7 (v1) [[User story 7 v1]](user_stories.md)

### 1. Title -- Manage Resources for Realistic and Challenging Gameplay 

### 2. Purpose -- As a user, I want to manage resources so that the simulation is realistic and challenging. 

### 3. Associated User Stories -- 7 (v1)

### 4. Actors -- The User

### 5. Preconditions -- The game includes a resource management system (e.g., funding, medical supplies, personnel). The simulation provides feedback on resource usage and availability. 

### 6. Main Flow -- regular flow of activities

#### Step 1 - The user starts with a set amount of resources displayed in the interface.  

#### Step 2 - The user allocates resources to different actions (e.g., deploying testing kits, hiring medical staff). 

#### Step 3 - The user monitors resource trends and adjusts strategies to avoid depletion. 

### 7. Alternative Flow -- exceptions to main flow

#### Exception 1 - If resources run low, the system provides alerts and suggests ways to obtain more (e.g., reallocating or prioritizing). 

### 8. Postcondition -- The resource management system adds depth to the gameplay, making it both realistic and challenging. 

