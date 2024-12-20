# Sprint 1: 2024-10-30 to 2024-11-05
Link to github repositories: https://github.com/orgs/CoralCoralCoralCoral/repositories

### Sprint Goal
The goal of this sprint is to create a first prototype for the game.

### Sprint Overview
###### We decided:
- We would go foward with the Epidemic Prevention game.
- To begin work on prototypes for the MVP.
- To start creating initial User Stories.

### Sprint Review
###### We decided:
- We should standardise our User Stories.
- Further work is needed on the prototypes.
- We needed to begin working on Use Cases.

### Sprint Retrospective
We had an intial idea of each team members strengths and areas of expertise. We realised that there was a large diversity of experience between team members in terms of tools used and familiarity with programming languages. Therefore, we had several options in terms of the software stack, as team members were open to which tools or programming languages were to be used. This gave us freedom to explore the most appropriate tooling and languages for the task at hand.

### Exception Handling
N/A

## Meeting Minutes

### Meeting 1 (Sprint Planning)
**Date:** 2024-10-30
**Place:** Workshop (5.13 CB)
**Objective:** Plan and discuss the development of a serious game.

### Discussion Points

##### Minimum Variable Product (MVP) and Sprint Goals
 
- Deliverables by Next Week:
- Develop a Minumum Variable product|(MVP), featuring a basic UI to demonstrate functionality.
- Ensure the MVP includes foundational elements such as a functional game UI connected to a local or server-side backend.
- Create a sprint documentation template.
##### Key features for the MVP:
- Browser-based game for accessibility and simpilicity.
- Local development preferred initially using HTTP servers or similar local setups.
- Simple UIs with graphical elements, even if the backend is not fully operational.

##### Technical Decisions
###### Architecture:
- Client-server model was considered, with potential use of WebSocket.
- We explored local developments versus server-based execution.

###### Platforms:
- Preference for cross-platform solutions but we leaned toward prioritising Windows for testing simplicity.

###### Languages and Tools:
- Options discussed include the use of Java, C++ and other lightweight frameworks for web development.
- Latex was preferred for documentation. 

##### Repository Management
###### Version Control:
- Main branches of repositories to be protected against direct push
- Require pull request with at least one approval from another team member before merging into main branch

###### Visibility
- Repositories may be made public for simpilicity and easy access.

##### Tasks for the Team
###### 1. Research Technologies
- Each member to research relevenat technologies/tools (e.g. game engines, UI libaries) by next meeting.
- Group discussion and decision-making  for next meeting.

###### 2. UI Design
- Create a simple mockup.
- Iterate on the design to align with MVP goals.

###### 3. Documentation
- Draft and refine sprint templates and project documentation.

###### 4. Sprint Workflow:
- Implement pair programming sessions for learning and development.
- Arrange optional in-person sessions for collaborative work.

##### Next Meeting Schedule
- **Date:** Saturday [02-11-2024]
- **Agenda:** Finalise technology decisions, UI mockups and distribute sprint tasks.
- **Ongoing Collaboration:** Use a mix of online and in-person sessions for effective teamwork.
  
---

### Meeting 2 
**Date:** 2024-11-02
**Location:** Teams


#### Agenda:
 
 1. Feedback review and next steps for project development.
 2. Simulation prototyping and framework setup.
 3. Sprint documentation and workflow.
 4. Schedule for next meeting.


### Discussion Points
##### Feedback Reviews and Recommendations:
We were advised by the customer to keep the initial prototype simple to ensure correctness and incrementally add complexities as we design the project.

##### Proposed Approach:
- Begin with a grid model where each square represents a value( e.g. density) impacting infection rates.
- Each agent should have one basic trait for simplicity.
- Test and refine the system iteratively.

##### Simulation and Technical Setup:
###### Development Tools:
- Backend: Spring Boots suggested for scaffolding; Rust can be used if necessary.
- Frontend: React recommended for UI development.
- Map integration: Plan to overlay a grid on a map using Mapbox.

###### Action Design for the prototype:
- Build a simple working model to simulate infection.
- Develop a basic UI with grid and map for next week's review.


##### Workflow and Sprint Documentation:
###### Next Action Plan:
- Use the provided TA documentation as a baseline for sprint tracking.
- Create initial tickets on Github.
- Establish a project repository for collarboration.

##### Next Meeting Schedule:
- Date and Time: 04-November-2024
- Location: University Campus
- Focus Areas:
  - Finalise Spring Boot setup and UI framework.
  - Review backlog items and documentation.

---

### Meeting 3 
Date: 2024-11-03
Place: Virgil Building
Participants: Koray Cooper and Umran Hussain

###### Meeting goals:
This meeting was to decide on the intial prototype.

###### Key Points:
- Intial UI mockups were discused. This would involve an interactive map that users could navigate to visulize the epedimic's state.

- Basic user actions such as lockdown, mask mandates, testing and infrastructure investment were considered.

- The details of the simulation model were also discussed. From this we decided on an agent based model, with spaces that agents would travel between. Spaces would have three variants: household, office or social space.

- For simplcity we assumed airborn transmission as the only infection vector.

- We proposed to simulate transmissions based on the [Wells-Riley model](https://en.wikipedia.org/wiki/Wells-Riley_model) of airborne transmission. 

- We proposed that agents would transition through infections states as laid out in the [SEIRS model](https://www.nature.com/articles/s41592-020-0856-2).

### Sprint 1 Customer Meeting

Four concepts were pitched to the customer during the meeting.

#### 1. Factory Simulation: Building a Net Zero Factory
 
###### Objective:
Develop a simulation game where the player assumes the whole of a factory manager, tasked with the role of building and expanding factory while balancing the growth of the factory with achieving net-carbon emission.
 
###### Mechanics:
- Players make strategic decision in offsetting carbon emissions and implementing green initiatives.
- Resources include money, political reputations, which can affect decision-making.
- The game introduces complexities and consequences to players' choices.
- Policies that are green-driven have to be optimized to balance profits and emissions, requring the players to juggle between priorities.
 
###### Feedback
 Customer acknowledged that while the concept was innovative, the scope for complexity is limited. 


#### 2. Epidemic Response Simulator

###### Objective:
 Create a real-world simulation game where the players act as public health officials managing an epidemic, using realistic models and interventions to contain the outbreak.

###### Mechanics:
- Players start with minimal information about the pathogen.
- Tools include public health interventions such as mask mandates, area lockdowns or vaccine development.
- Introduces randomness to simulate real-world probability.
- Decisions lead to random outcomes based on demographics, efficacy and public compliance.

###### Feedback:
Customer agreed that the concept strongly alligns with serious game and might appeal to the intended target audience such as health students and health decision makers. 

#### 3. De-escalation Training Simulator

###### Objective:
 A simulation aimed at training users in de-escalating volatile scenerios, such as handling distressed individuals or angry customers.

###### Mechanics:
- Sceneario-based interactions where players are prompted to choose multiple dialogues or action to de-escalate situation.
- Preamble about what has happened, and player given a brief.
- Different scenerios could include customer service challenges in workplace, hospitals, and public events.
- Potential integration of AI to generate dialogues and responses.

###### Feedback:
Customer found it more intriguing than what was attempted last year if there is the technical expertise within the group to realise it. A plethora of online learning materials also makes it more feasible.

#### 4. Bath Go:
###### Objective:
An augumented reality game that combines geo-location with trivia and collectible mechanics, inspired by Pokemon Go.

###### Mechanics:
- Players explore Bath and its surrounding areas to discover landmarks, restaurants, shops, etc whilst collecting virtual cards.
- Cards could include historical, cultural or practical  information about the location.
- Gamification elements like completing levels and using collectible cards accrued for competitive play.

###### Feedback:
Runs the risk of oversimplification of serious games and might not be otherwise considered a serious game.


##### General meeting feedback from customer and next steps:
- Most promising concepts were both Epidemic Response Simulator and De-escalation Training Simulator, due to their alignment with serious games and their potential impacts. 

- Customer advised that ideas be further evaluated and narrow down choices by next meeting. 
 
 
