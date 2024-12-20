# Sprint 4: 2024-11-20 to 2024-11-26

### Sprint Goals
Work on the simulation-engine to would improve its realism and further develop the UI to include a interactive map.

### Sprint Overview
##### We wanted to:
- Introduce surveillance actions, such as: 
   - Testing in healthcare spaces.
   - Home testing kits where agents could test themselves in their household space.
   - Waste water testing.
- Introduce intervention actions, such as:
   - Masks mandates.
   - Lockdowns.
- Introduce research actions that the user could take to unlock more effective interventions and surveillance.
- Introduce the concept of jurisdictions, so that players could selectively apply polices to specific geographic locations.

- Allow users to interact with the simulation-engine using the UI.

### Sprint Review
- Created the concept of jurisidictions by modeling them after Local Authority Districts and the MSOAs within them. We used government cencus data for this.

- Extended angent states to represent hospitalisation and death.

- Modified the simulation model to have each space (households, offices, social, healthcare) allocated to a jurisdiction based on population density data taken from the census. 

- Created a new type of space called the healthcare space. This was done so that we could later introduce surveliance processes and also model hospitalisations.

- Created intervention actions, such as mask mandates and lockdowns, which could be applied at the jurisdiction level.

- Made progress towards connected the UI and the simulation-engine, but this would need further work in the next sprint.

### Sprint Retrospective
We started to become more comfortable with each other and our existing work flow and were happy to carry on without major changes.

We did not have a fully integrated playable game at this point. Therfore, the focus of the team became about delivering a playable game as soon as possible.

### Exception Handling
N/A

---

## Meeting Minutes

### Meeting 1 (Sprint Planning)
**Date:** 2024-11-20
**Location:** Unrecorded
**Attendees:** Team Coral

### Discussion Points
- Need to do detailed documentation of retrospective meetings.

- Prioritisation of sprint documentation.

- Ensure all documentations are cohesive and ready for assessments.

- Define clear acceptance cretaria for each user story.

- Link user stories to corresponding use cases.

- Ensure each user stories include multiple use cases to illustrate different scenarios.

- Clarify the states of each task at the end of the sprint.

- Review user stories and ensure all taks have defined owners and states.

##### Next Meeting Schedule
**Date:** 2024-11-23
**Agenda:** Establish a consistent format for sprint documentation and ensure ongoing tasks are properly documented and tracked.

---

### Meeting 2
**Place:** Teams 
**Date:** 23/11/2024 2024-11-23
**Attendees:** Team Coral 

#### Agenda

1. Review of Oracle use cases.
2. State transition modelling.
3. UI and Provinces Data Model.
4. Front-End and Backend integration.
5. Deployment Repository and Build Processes.


#### Review of Oracle Use cases

**Purpose:** Design oracle use cases to notify users about critical threshold and provide actionable advice.

**Example:** When hospital capacity exceeds 90%, the Oracle:
- Pause the game.
- Informs the user of the situation and suggests a lockdown.
- Offer additional details or alternative actions.


#### State Transition Modelling
**Current states:** 
- Not Infected
- Infected
- Ill 
- Dead

**Proposed additional states:** 
- Hospitalised 
- Deceased

#### Discussion Points
- Introduce variable stochastic probabilities for hospitalisation and recovery time based on agent's health state.
- Model healthcare workers as a separate category.
- Hospitals as potential infection spread hubs, especially during early outbreaks.

##### UI and Provinces Data Model
- A sidebar to display available actions with future plans to add localized actions.

- Development underway to introduce a structure for jurisdictions.

- Simplified dropdown implementation for initial testing.


##### Frontend and backend integration

- Successfully displaying UI on servers

- Progress on web socket integration for message transmission between frontend and backend.


##### Deployment Repository and Build processes

- Current method involves manual build and development of the front end.

- Proposal to automate the build process using GitHub actions and integrate it into the deployment repository.

- Set up a deployment repository for modularity.

- Exclude build versions of the UI from the API server repository.


##### Next Step
- Continue refining Oracle use cases and state transitions.
- Finalizse provinces data model and actions UI.
- Integrate automation for front-end deployment.
- Prepare healthcare worker modelling for next sprint.

### Customer Meeting and Analysis

**Date:** 2024-11-20
**Location: Unrecorded**
**Attendees:** Customer and Team Coral

#### Agenda

1) UI Development Status
2) Simulation Infrastructure and Data Processing
3) Next Sprint Goals
4) Customer Feedback and Clarification
5) Discussion on Oracle Implementation


#### Meeting Summary

##### UI Progress:
- Interactive map framework completed but does not yet display simulation data.
- Planned functionality includes displaying infection statistics by location and enabling historical searches.

##### Backend Infrastructure:
- Developed infrastructure for simulation event handling, including:
   - **Message Queues:** For efficient communication between UI and Simulation.
   - **Elastic Search:** For indexing simulation data to facilitate historical searches via REST API.

##### Concrete User Actions:
 Established a list of actionable user interactions for implementation in the next sprint.

#### Customer Feedback
##### Functionality expectations:
- Focus on achieving core functionality before expanding features.
- Deliver a fully playable system with clear start, middle and end.
 
##### Custom Scenarios
- Current focus on predefined scenarios is acceptable
- Highlight in documentation how the system can be extended for custom scenarios in the future

##### Documentation Suggestions:
- Include modular design consideration to demonstrate potential tweak for future enhancements
- Document unimplemented features as potential improvements.

##### Oracle Design
- The oracle should assist without making them too reliant.
- Consider a scalable Oracle model, potentially adaptable based on user experience levels.


##### Challenges and Concerns
 Concern about delivering the perfect game was raised. Customer wants the team to prioritize playability and core functionality over perfection.
 Frontend-backend connection not complete. Customer wants integration.


##### Action Plan for Next Sprint
 1. UI Integration
 2. Implement user actions  for interacting wit the game
 3. Develop a reactive Oracle to provide contextual advice based on game states.
 4. Ensure the Oracle system is modular and extendable for future refinements.
 5. Test and debug the core gameplay loop to ensure stability and usability. 
