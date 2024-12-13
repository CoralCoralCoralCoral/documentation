
# Use Cases

**Title:** Geo Visualisation of Jurisdiction

**Purpose:** Display the Local Authority Districts and MSOA contained within them, visualised on a map.

**Purpose:** As a user, I want to implement actions within a given geographic scope so that I can use resources efficiently.

**Actors:** 
- System
- User

**Preconditions:**  Data for LAD and MSOA is loaded onto the UI. 

**Main Flow:** Regular flow of activities.

- **Step 1** -  UI map shows the outlines for the LADs.

- **Step 2** - The User selects a LAD.

- **Step 3** - The System zooms into the LAD and displays the MSOAs within the LAD.

- **Step 4** - The system updates the simulation to reflect the effects of the action in the chosen area. 

**Alternative Flow:** Exceptions to main flow.

**Postcondition:** Actions are successfully applied within the specified geographic scope, optimizing resource use. 

**Test:** 
- **Step 1:** Check if LAD outlines are displayed on the map. If not FAIL.
- **Step 2:** Select LAD. Check if the currently selected LAD is the LAD that was selected. If not FAIL.
- **Step 3:** Check if the map state has been updated to reflect the selected LAD. If not FAIL.
- **Step 4:** Check if map zooms to the bounds of the selected LAD. If not FAIL.
- **Step 5:** Check if the outlines of the MSOAs within the LAD are displayed on the map. If not FAIL. 

---

## 6 (v1) [[User story 6 v1]](user_stories.md)

**Title:** Implement Actions Within a Geographic Scope

**Purpose:** As a user, I want to implement actions within a given geographic scope so that I can use resources efficiently

**Associated User Stories:** 6 (v1)

**Actors:** User

**Preconditions:** The map displays distinct geographic regions with selectable areas. The system supports targeted actions such as testing, lockdowns or resource distribution. 

**Main Flow:**  Regular flow of activities.
- **Step 1** - The user selects a specific region on the map. 

- **Step 2** - The system highlights the chosen region, showing relevant data (e.g. infection rates, available resources). 

- **Step 3** - The user implements an action (e.g. deploying a testing strategy or imposing restrictions) within the selected region.

- **Step 4** - The system updates the simulation to reflect the effects of the action in the chosen area. 

**Alternative Flow:** Exceptions to main flow.

**Exception:** If the user tries to apply actions to an unselected region, the system provides a prompt to select a scope first.  

**Postcondition:** Actions are successfully applied within the specified geographic scope, optimising resource use.

**Test:** 
- **Step 1:** Select a region on the map.
  - Does the region get highlighted. If not FAIL.
  - Does the region's metrics get shown on the sidebar. If not FAIL.
- **Step 2:** Implement a policy. Does the sidebar show that the policy is active. If not FAIL

---

### 7 (v1) [[User story 7 v1]](user_stories.md)

**Title:** Manage Resources for Realistic and Challenging Gameplay

**Purpose:** As a user, I want to manage resources so that the simulation is realistic and challenging.

**Associated User Stories:** 7 (v1)  

**Actors:** User  

**Preconditions:** The game includes a resource management system (e.g., funding, medical supplies, personnel). The simulation provides feedback on resource usage and availability.

**Main Flow:** Regular flow of activities.

- **Step 1** - The user starts with a set amount of resources displayed in the interface.

- **Step 2** - The user allocates resources to different actions (e.g., deploying testing kits, hiring medical staff).

- **Step 3** - The user monitors resource trends and adjusts strategies to avoid depletion.

**Alternative Flow:** Exceptions to main flow.

**Exception:** If resources run low, the system provides alerts and suggests ways to obtain more (e.g., reallocating or prioritizing).

**Tests:**

- **Test 1 - Action Costs**
  - **Step 1:** Check to see if resources are visable on UI. If not FAIL.
  - **Step 2:** Check if actions have visable resource cost. If not FAIL.
  - **Step 3:** Implement an action. Check to see if resources are deducted by expected amount. If not FAIL.

- **Test 2 - Running Costs**
  - **Step 1:** Run game.
  - **Step 2:** Implement testing.
  - **Step 3:** Check to see if resources are deducted regularly by expected amount. If not FAIL.
  

