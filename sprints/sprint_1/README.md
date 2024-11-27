# Sprint 1: 2024-10-30 to 2024-11-05

## Overview
We decided that we would go foward with the epdidemic prevention game.

We decided to work on prototypes for the MVP.

We started to create initial User Stories.

## Review
We decided that we should standardize our user stories.

We needed further work on the prototypes.

We needed to start working on use cases.

## Meeting Minutes

### Meeting 1 (Wednesday 2024-10-30, Workshop)
// Team Name: Coral
Date: 30-10-2024
Objective: Plan and discuss the development of a serious game.

Discussion Points

1. Minimum Variable Product(MVP) and Sprint Goals
  
   . Deliverables by Next Week:
   .Develop a Minumum Variable product|(MVP), featuring a basic UI to demonstrate functionality.
   .|Ensure the MVP includes foundational elements such as a functional game UI connected to a local or server-side backend.
   . Create a sprint documentation template.

.Key feathures for the MVP:
 .Browser-based game for accesssibility and simpilicity
 .Local development preferred initially using HTTP servers or similar local setups
 .Simple UIs with graphical elements, even if the backend is not fully operational

2. Technical Decisions
 .Archictecture:
  .Client-server model was considered, with potential use of Websocket.
  .We explored local developments versus server-based execution.
 .Platforms:
  .Preference for cross-platform solutions but we leaned toward prioritising Windows for testing simplicity.
 .Languages and Tools:
  .Options discused include the use of Java, C++ and other lightweight frameworks for web development.
  .Latex was preferred for documentation. 

3. Repository Management
 . Version Control:
  .Main branches of repositories to be protected against direct push
  . Require pull request with at least one approval before merging into main branch
 .Visibility
  .Repositories may be made public for simpilicity and easy access.

4. Tasks for the Team
 1. Research Technologies
  . Each member to research relevenat technologies/tools (e.g. game engines, UI libaries) by next meeting.
  . Group discussion and decision-making  for next meeting.
 2. UI Design
  . Create a simple mockup.
  . Iterate on the design to align with MVP goals.
 3. Documentation
  .Draft and refine sprint templates and project documentation.
 4. Sprint Workflow:
   . Implement pair programming sessions for learning and development.
   .Arrange optional in-person sessions for collarborative work.

5. Meeting Schedule
  .Date: Saturday[02-11-2024]
  . Agenda: Finalise technology decisions, UI mockups, and distribute sprint tasks.
 .Ongoing Collaboration:
  .Use a mix of online and in-person sessions for effective teamwork.
  

### Meeting 2 (Saturday 2024-11-02, Teams)
    Date: 02-November-2024
     Time: 14:00
     Platform: Teams


Agenda:
 
 1. Feedback Review and Next steps for Prjoect develpment

 2. Simulation prototypying and Framework stepup

 3. Sprint Documentation and Workflow

 4. Schedule for Next meeting


 Key Discussions
  1.Feedback Reviews and Recommendations:
   We were adviced by the customer to keep the initial prototype simple to ensure correctness, and incrementally add complexities as we design the project.
  Proposed Approach:
   .Begin with a grid model where each square represents a value( e.g., density) impacting infection rates.
   . Each agent should have one basic trait for simplicity.
   .Test and refine the system iteratively.

   2. Simulation and Technical Setup:

     . Development Tools:
      .Backend: Spring Boots suggested for scaffolding; Rust can be used if necessary.
      .Frontend: React recommended for UI development.
      .Map integration: Plan to overlay a grid on a map using Mapbox.
    Action Design for the prototype:
     .Build a simple working model to simulate infection.
     . Develp a basic UI with grid and map for next week's review.


   3. Workflow and Sprint Documentation:
    . Next Action plan
     . Use the provided TA documentation as a baseline for sprint tracking.
     .Create initial tickets on Github.
     .Establish a project repository for collarboration

   4. Schedule Planning for Next Meeting:
    . Date and Time:04-November-2024
    . Location: On Campus
    .Focus Areas
     .Finalise Spring Boot setup and UI framework.
     . Review backlog items and documentation.




















### Meeting 3 (Sunday 2024-11-03, Virgil Building)

## Backlog

-   Set up sprint documentation format
-   Set up documentation repository
-   Set up sprints and kanban board
-   Develop initial customer stories
-   Develop prototype

### Complete Backlog Tasks

-   Set up sprint documentation format
-   Set up documentation repository
-   Set up sprints and kanban board
-   Develop initial customer stories

### New Backlog Tasks

-   Develop prototype

## Exception Handling

## Product Documents

### Customer Meeting and Analysis


Sprint 1 Customer Meeting

Four concepts were pitched to the customer during the meeting. 

1. Factory Simulation: Building a Net Zero Factory
 
 Objective:
  Develop a simulation game where the player assumes the whole of a factory manager, tasked with the role of building and expanding factory while balancing the growth of the factory with achieving net carbon emission.
 
 Mechanics:
 . Players make strategic decision in offsetting carbon emissions and implementing green initiatives
 . Resources include money, political reputations, which can affect decision-making.
 .The game introduces complexities and consequences to players' choices.
 .Policies that are green-driven have to be optimized to balance profits and emissions, requring the players to juggle between priorities.
 
 Feedback
 Customer acknowledged that while the concept was innovative, the scope for complexity is limited. 


2. Epidemic Response Simulator

 Objective:
 Create a real-world simulation game where the players act as public health officials managing an epidemic, using realistic models and interventions to contain the outbreak.

 Mechanics:
 . Players start with minimal information about the pathogen 
 . Tools include public health interventions such as mask mandates, area lockdowns or vaccine development.
 . Introduces randomness to simulate real-world probability
 . Decisions lead to random outcomes based on demographics, efficacy and public compliance.

 Feedback:
 Customer agreed that the concept strongly alligns with serious game and might appeal to the intended target audience such as health students and health decision makers. 

3. De-escalation Training Simulator

 Objective:
 A simulation aimed at training users in de-escalating volatile scenerios, such as handling distressed individuals or angry customers.

 Mechanics:
 . Sceneario-based interactions where players are prompted to choose multiple dialogues or action to de-escalate situation.
 .Preamble about what has happened, and player given a brief.
 . Different scenerios could include customer service challenges in workplace, hospitals, and public events.
 .potential integration of AI to generate dialogues and responses.

 Feedback:
 Customer finds it  intriguing than what was attempted last year if there is technical expertise within the group to actualise it. A plethora of materials online also makes it more feasible.

4. Bath Go:
 Objective:
 An augumented reality game that combines geo-location with trivia and collectible mechanics, inspired by Pokemon Go.

 Mechanics:
 .Players explore Bath and its surrounding areas to discover landmarks, restaurants, shops, etc whilst collecting virtual cards.
 .Cards could include historical, cultural or practical  information about the location.
 .Gamification elements like completing levels and using collectible cards accrued for competitive play

Feedback:
 Runs the risk of oversimplification of serious games and might not be otherwise considered a serious game.


General Meeting Feedback from Customer and Next steps
 Most promising concepts were both Epidemic Response Simulator and De-Escalation Training Simulator, due to their allignment with serious games and their potenetial impacts. 
 Customer adviced that ideas are furtehr evaluated and narrow down choices by next meeting. 
 

 

### User Stories

### User Cases

