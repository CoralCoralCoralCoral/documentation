# Sprint 5: 2024-11-27 to 2024-12-03

## Sprint Goal
The goal of this sprint was to put together a playable game.

## Sprint Overview
We wanted to:
- Implement surveillance processes in the simulation-engine.
- Have the UI talking to the simulation-engine. 
- Be able to display the real-time metrics on the UI.
- Be able to geographically visualize the epidemic's state on the map.
- Have the user be able to take surveillance and intervention actions by interacting with the UI.
- We wanted to implement the oracle. This was a lower priority for this sprint.

## Sprint Review
- Sucessfully implemented the simulation of healthcare space based testing, which produces surveillance metrics.
- Implemented a "start game" button in the UI which would intiate a new game, by sending a message to the simulation-engine.
- The UI able to recieve metrics aggregated by jurisdiction from the simulation-engine.
- UI map is able to visualise the epidemic's state based on the metrics received from the simulation-engine.
- UI is now able to generate and display graphs based on the metrics received from the simulation-engine.
- Although the simulation engine was setup to recieve and handle surveillance and intervention actions, due to a de-serialisation bug in the messaging layer, the UI was not able to send these message.
- The Oracle was not implemented in this sprint, thus was left for the next sprint.


## Sprint Retrospective
Although we were able to integrate most aspects of the UI and simulation-engine, the bug that prevented user actions from being sent to the simulation-engine prevented the game from being in a playable state. This was a huge disappointment for the team and we recognised that discovering these types of bugs at the last minute is not ideal. In order to prevent bugs of this class in the future, we decided to write automated unit tests for all serialisation and deserialisation logic.

## Exception Handling
We discovered a bug in the deserialisation of "command" messages sent from the UI to the simulation-engine, which resulted in these messages being ignored by the simulation-engine. This prevented us from achieving the goal of enabling bi-directional communication between the UI and simulation-engine. This issue was caught during manual integration testing at the very last minute before the demo. This bug would eventually be fixed in the next sprint.

---

## Meeting Minutes

### Meeting 1
**Date:** 2024-11-27
**Participants:** Team Coral
**Location:** University of Bath

#### Agenda

1. Review of simulation flow and gameplay mechanics.
2. Updates on jurisdictions, space allocation, and healthcare modeling.
3. Discussion of metrics and debugging for the simulation.
4. Documentation and deliverables.

#### Discussion Summary

##### Simulation Flow and Gameplay Mechanics

- **Gameplay Flow:**
    - The simulation should balance decision-making pauses with fast-forward gameplay for efficiency.
    - Users are expected to pause gameplay for deliberation and decision-making, followed by simulation resumption to observe outcomes.
    - The team discussed adding a feature to simulate and store decisions for predefined periods (e.g. two weeks) to improve user experience.

- **Decision on Pausing:**
    - Pausing allows users to review statistics and decide on actions without affecting gameplay consistency.
    - Pre-simulating events during pauses could be an option but requires careful alignment with decision-making logic.


##### Updates on Jurisdictions and Space Allocation

- **Jurisdiction-Based Modeling:**
    - Jurisdictions are defined based on MSOAs (Middle Super Output Areas), with parent-child relationships mapped for scalability.
    - Spaces (e.g., houses, offices, healthcare facilities) are distributed within jurisdictions based on population density and census data.

- **Space Characteristics:**
    - Population weights for allocation.

    - Categories such as households, offices, and shops.

    - Healthcare facilities with bed capacities derived from averages (e.g. 5 beds per 1,000 people for the UK).

    - Potential to refine space allocation using geographic coordinates or more detailed census data.

- **Healthcare Facilities:**
    - Healthcare spaces modeled with variance in capacity for realism.
    - Limited modeling of healthcare facilities in the current simulation for London.



##### Metrics and Debugging

- **Metrics Captured:**

    - New infections, hospitalizations, recoveries, deaths.

    - Current states (infected, infectious, hospitalized, deceased).

- **Simulation Functionality:**

    - Jurisdictions, space allocation, and agent movement have been tested.

    - Debugging focused on memory and latency issues, particularly when scaling up agent numbers.

- **Simulation Adjustments:**

    -  Introducing probabilities for hospitalization and fatalities to reflect real-life disease progression.

    - Adding relationships between agents (e.g. household or social connections) to simulate realistic behaviors, such as visiting hospitalized individuals.

##### Documentation and Deliverables

-  **Focus on Documentation:**
    - Team highlighted the need for comprehensive sprint documentation to capture internal meetings and outcomes.
    - Ensure alignment with official coursework requirements by clarifying expectations with the supervisor.

- **Tools for Documentation:**
    - Utilise GitHub and shared repositories to manage and version-control simulation-related documents and code.



##### Challenges and Solutions

- **Challenges:**

    -  Balancing simulation complexity with ease of debugging.

    - Incorporating realistic healthcare and spatial dynamics without overwhelming computational resources.

    - Defining gameplay flow that is engaging and aligns with user expectations.

- **Proposed Solutions:**

    - Incremental implementation: Start with simplified models and add complexity step-by-step.

    - Optimise memory usage to support larger agent populations.

    - Focus on visualizing key metrics for decision-making while streamlining background computations.



##### Next Steps

**1. Refine Simulation:**

- Enhance jurisdiction-based space allocation.

- Improve agent movement logic and metrics collection.

- Optimise performance for larger populations.

**2. Develop Gameplay Features:**

- Implement real-time decision-making and pausing logic.

- Add predictive features to allow users to pre-simulate outcomes.

**3. Documentation and Communication:**

- Finalise sprint documentation and ensure alignment with coursework guidelines.

- Share progress updates with supervisors and obtain feedback for adjustments.

---

### Meeting 2
**Date:** 2024-11-30
**Participants:** Team Coral
**Place:** Online/In-person

#### Agenda:

1. Testing procedures and structure.
2. Finalising backlog actions.
3. UI development and API server integration.
4. Documentation updates and formatting.

#### Discussion Points

##### Testing for Use Cases:
- A test will be created for each use case, focusing on verifying the expected outcomes for varied inputs.
- Tests are designed to ensure the flow and implementation correctness by validating preconditions and postconditions.

##### Testing Documentation:
- A new section, “Testing Procedures,” will be added to the sprint documentation.
- This section will outline test cases for each use case, highlighting different branches and scenarios.

##### Approach to Testing:
- Not every step of a use case will be individually tested; instead, tests will focus on key user interactions and outcomes.
- Tests will evaluate different variable inputs and ensure consistent behaviour across scenarios.

#### Sprint Backlog and Progress

##### Backlog Prioritisation: 

- Basic actions are prioritised for early completion in the sprint to allow more focus on advanced features later.

- Simulation changes will be restricted to necessary adjustments, with a focus on locking down existing functionalities.

##### Key Deliverables:

- Finalising UI components and integrating them with the API server.

- Refining CRC (Class Responsibility Collaborator) cards to document system interactions and dependencies.

- Creating documentation for installation and user manuals.

#### UI and API Server Integration
##### UI Development:

- The primary sprint focus is on making the UI functional and interactive.

- The UI will be integrated with the API server to display metrics and manage global state (e.g., selected jurisdiction, received metrics).

##### State Management:

- State management (e.g., using Redux or similar) will be implemented to track and update metrics without race conditions.

- UI elements will update daily based on data received from the simulation service.

##### Collaborative Efforts:

-  Team members expressed interest in contributing to UI development, particularly in creating and managing game configurations.

#### Documentation Updates

##### Documentation Status:

- Documentation for previous sprints (especially Sprint 1) is being reviewed and refined to ensure consistency.

-  Retrospective use cases and user stories from earlier sprints are being integrated into the correct sections.

##### Installation and User Manuals:

- A simplified installation guide will focus on Docker-based setup instructions:
    -  Download the necessary files.
    -  Run Docker.
    -  Access the application via a browser.
    -  The user manual will detail key parameters, configuration steps, and basic gameplay instructions.

##### Linking Documents:
- References to user stories and use cases will be linked within the documentation for easy navigation.
- Markdown syntax will be used to create clean, accessible links.

#### Decisions and Next Steps
##### Decisions:

- **Testing:** A structured yet flexible approach to testing will be documented and implemented.

- **Backlog:** Lock down simulation features and shift focus to UI and documentation.

##### Next Steps:

1. **Testing Procedures:** Document test cases for all use cases in the “Testing Procedures” section.

2. **UI Development:** Complete UI functionality and integrate with the API server.

3. **Documentation:** Finalise and merge all pending documentation, including user manuals and sprint-specific updates.

4. **Collaboration:** Team members to meet on Saturday to finalise deliverables and align on sprint objectives.



#### Action plan for next Sprint

- Tasks Assigned To Deadline Status.
- Document test cases for use cases Team Member(s) by Sprint End In Progress.
- Finalise UI-API integration UI Team Next Meeting Ongoing.
- Refine CRC cards Documentation Team Next Sprint Pending.
- Complete installation guide Documentation Team by Sprint End In Progress.

---

### Customer Meeting and Analysis
**Date:** 2024-11-27
**Attendees:** Customer and Team Coral

#### Sprint Goals:
- Share progress on the game project.
- Discuss challenges related to data accuracy and performance.
- Identify the next steps for front-end and back-end integration.

#### Key Discussion Points
##### Project Purpose:
The primary objective of the meeting was to showcase the progress made in game mechanics, including a functional UI.

##### Progress Achievements:
- Successfully integrated data from the Office for National Statistics (ONS) for population density.
- Focused on London’s data for initial implementation.
- UI improvements are in progress.

##### Data Integration:
- Utilized ONS census data to determine population densities and local authority districts (LADs).
- Implementation goes as fine-grained as output areas but avoids individual postcodes for efficiency.

##### Population Density and Space Allocation:
- Spaces (residences, offices & social areas) are allocated based on population density:
- More dense areas → More spaces.
- Less dense areas → Fewer spaces.
- Plans to aggregate metrics at LAD and Middle Layer Super Output Area (MSOA) levels.

##### Simulation Challenges:

- Running simulations with 1 million agents causes delays (8 seconds for a game day).
- Computational load is significant, especially for large populations.

##### Proposed Solutions:
- Adjusting the simulation time step (from 15 minutes to 1 hour) to reduce load.
- Optimising simulations for high-performance environments or cloud services.
- Introducing representative agents (one agent representing multiple people).



#### Architecture Overview:

##### Simulation Service:

- Separate from the front end.

- Can be run on high-performance servers or laptops, depending on the user’s resources.

- Designed for scalability and university-level usage.

##### Front-End/Back-End Integration:
- **Current Status:**
    - Core back-end functionalities are in place.
    - Front-end integration is ongoing.

- **Next Steps:**
    - Complete integration to allow user actions in the UI.
    - Focus on making the UI more interactive in the next sprint.



#### Challenges and Action Items:

##### Challenges Identified:
- Scalability and performance optimization.
- Ensuring accurate simulations while reducing computational load.
- UI and back-end communication delays due to mapping tasks.

##### Action Items for the Next Sprint:

- **UI Focus:** Complete integration of user actions into the front end.

- **Optimisation:** Explore cloud deployment and representative agent strategies.

- **Testing:** Conduct small-group tests for potential deployment options.

- **Documentation:** Improve internal documentation to streamline development processes.

##### Next Steps and Review Plan:

- **Short-Term:** 
    -   Focus on UI interactivity and system optimisation.
    -  Address scalability issues with high-density simulations.

- **Long-Term:**
    - Continue testing and refining simulations.
    - Document progress thoroughly to enhance team collaboration.

##### Meeting Conclusion:

-  The team acknowledged current challenges and outlined clear steps to address them.
-  Progress will be reviewed in the next sprint, focusing on integration, testing, and optimisation.