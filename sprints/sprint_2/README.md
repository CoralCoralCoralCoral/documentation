# Sprint 2: 2024-11-6 to 2024-11-12

### Sprint Goal
The goal for this sprint was to visualize a basic simulation.

### Sprint Overview
###### We wanted to create:
- a basic UI showing a map for the game.
- a basic model of a simulation.

### Sprint Review
- A mockup of the UI was done. Actual implementation was left for next sprint.
- A functional agent based simulation model was built.

### Sprint Retrospective
Due to some teammates missing without prior warning. We ended up in a situation where only one team member was present at the customer meeting. We came to the understanding that notice should be given where possible.

We had decided on which tools and languages that we were going to use moving forward. The initial simulation model was built in Golang and it seemed like a good fit for the purpose, thus team members decided to stick with it going forward. One implication of this decision was that we would have to maintain a separate repository for the simulation model, thereafter refered to as simulation-engine. Since Golang is not necessarily the best langauge for UI development, we also decided to create a seperate repository for the UI, which would be built using JavaScript.

### Exception Handling
Issue of missing customer meeting was raised. We decided that better team co-ordination was required and that this was a one-off due to a mix of planned absences coinciding with illness.

## Meeting Minutes

### Meeting 1 (Sprint Planning)
Date: 2024-11-09
Place: Teams

### Discussion Points
- Meeting started by referencing feedback from customer.
- Key suggestions from customer include:
  - Start Simple, avoid making the simulation too complex from the onset.
  - Begin with minimal variables to ensure correctness.
  - Add complexity step-by-step, testing each addition thoroughly.
  - Develop a functional base before experimenting with advanced features.
  - Use existing frameworks for efficiency.

##### Based on the feedback from customer, several issues were highlighted:
- Focusing on creating simple grid-based simulation.
- Each grid square will have a "density" value affecting infection rates.
- Infection chances influened by both agent traits and grid varaiables.

###### Frontend Development:
 - Use react for frontend as many team members are familiar with it.
 - plan to integrate Mapbox to visualize the grid.
 - Deliver a simple UI by next week to showcase initial functionality.

###### Backend framework:
- Recommendation to use Spring Boot for backend scaffolding to avoid unnecessary complexity.
- Ensure ease of integration with other components.

###### Action Plan:
- Create an initial grid simulation
- Set up GitHub repository for collaboration and issue tracking.
- Develop a UI showcasing grid functionalityand agent interactions.
- Prepare initial tickets for backlog to focus team efforts.
- Use the provided template for sprint documentation.

##### Next Meeting Schedule:
**Date:** Monday (2024-11-11)
**Agenda:**
- A functional backend setup (Sprint Boot Scaffolding) by next meeting.
- Initial UI with a grid overlay and basic agent interactions.
- Updates to backlog and sprint documentation.
- Feedbacks on user stories and design will be shared iteratively.

##### Conclusion
 The team  took the customer's advice on board by focusing on simplicity and making improvements as the game development advances. Also discussed different ways to collaborate to ensure team is on track with a clear roadmap for next sprint. 

---

### Meeting 2 
**Date:** 2024-11-11
**Place:** School of Management

#### Agenda:
1. Review of sprint documentation.
2. Updates on ongoing project components.
3. Discussion of feedback and next steps.


### Discussion Points
##### Sprint Documentation

**Decision:** Use the existing documentation template provided by the TAs with minor rearrangements to fit team requirements.

**Key sections to include:**
- Overview.
- Summary and review of sprint progress.
- Minutes and backlog snapshots (beginning and end of sprint for comparison).

**Formatting:**
- Markdown was suggested for its ease of use over LaTeX.
- Links to Google Docs and GitHub for recordings, backlog items, and other relevant documents.

**Action Items:**
- Finalise documentation for the last sprint and ensure consistency across all future sprints.
- Include sections for code updates and user stories.

#### Sprint Activities and Updates
**UI Development:**
- A basic user interface (UI) was developed.
- Tools Used: Not specified.
- UI showcased a map-based grid allowing users to view statistics and take actions.
- UI elements:
  - Map for geographic representation.
  - Global and local statistics (e.g. hospital capacity, GDP, vaccination rates).
  - Action menu for implementing policies (e.g. mask mandates, lockdowns).

**Simulation Model:**
- Spaces categorized into households, offices and social spaces with attributes like capacity, ventilation rate and infectious doses.
- Population assigned to households, with agents moving based on probabilities determined by a Markov process.

**Infection Dynamics:**
- Agents move between spaces, potentially spreading infection based on their state (susceptible, infected, infectious, immune, or dead).
- States transition probabilistically and are influenced by variables like pathogen characteristics and ventilation rates.

**Results:**
- Early tests showed exponential infection rates with stabilizations under lockdown scenarios.
- Basic metrics (e.g., daily infection counts, GDP impact) generated for analysis.

**Pathogen Modeling:**
- Characteristics such as emission rates, recovery periods and immunity durations modeled for different pathogen profiles.
- Infection probabilities calculated using Bernoulli distributions.

**Data Streaming:**
- Simulation data designed to stream events, allowing integration with Spring Boot systems for further analysis and visualization.

#### Challenges and Feedback

**Feedback from Advisors:**
- Keep simulations simple initially to identify errors and validate results.
- Incrementally add complexity after validating foundational models.

**Challenges:**
- Balancing complexity with clarity.
- Handling computational efficiency for large-scale simulations (e.g. 400,000 agents).

#### Next Steps

**Development:**
- Refine the simulation model to ensure accuracy and simplicity.
- Enhance the UI to integrate with real-world data (e.g. GIS mapping).
- Add roles and movement patterns for agents to reflect realistic behaviors.

**Documentation:**
- Complete and submit sprint documentation for past and current sprints.
- Standardise the format to streamline future updates.
- Collaboration:
- Establish workflows for integrating team contributions via GitHub.
- Schedule follow-up meetings to review progress and refine tasks.

**Key Decisions:**
- Use Spring Boot for backend management and GIS data for map-based modeling.
- Adopt a phased approach for simulation development:

  1. Start with a simple grid.

  2. Gradually incorporate additional variables like ventilation and transit spaces.

- Prioritise resource management in the simulation to reflect real-world scenarios (e.g. GDP impacts, hospital capacity).

### Customer Meeting and Analysis
- Concerns were raised over how many members of the group were missing. This was dealt with later, and explanations were made for those group members missing. Group members had communicated about abscenses over the previous Sprint, a couple illnesses meant there was less members available for the Customer meeting.

- The group explained that they chose to work on the epidemic response game rather than the de-escalation training game.

- Mechanics for how we would simulate the spread of a disease using the agent model was explained to the customer and how we would map where agents were using spaces. Feedback from this was to keep the simulation simple to begin with as it could be hard to implement and if we start to complex then we will not be able to tell if the simulation is working and which parts are not working.

- Basic user story and model was shown to the customer and the feedback given was to chose an already established UI system rather than build our own as that could be quite complex.

- Overall feedback was to start with a simple model to begin with and if we have time to expand upon that simple model.

