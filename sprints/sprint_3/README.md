# Sprint 3: 2024-11-13 to 2024-11-19

## Sprint Goal
The goal of this sprint was to implement a functional UI.

## Sprint Overview
We wanted to create a working UI.

We wanted to have the API server commmunicate with the simulation engine.

We wanted to come up with a design specification for the oracle.

## Sprint Review
Initial iteration of the UI was completed, which included a basic layout of the UI. We decided to integrate the map with the UI in the next sprint.

We created an API server that would sit inbetween the client and the simulation engine.

We have a intial design specification for the oracle. 

## Sprint Retrospective
Since we were dealing with a lot more integration task (having the UI stream updated from the simulation engine for example). We did pair programming between team members that were primarily responsible for different aspects of the code (e.g. UI devs worked with simulation engine devs).

## Exception Handling
Simulation engine produces too much data to be stored on the clientside, if we decided to send updates on every tick. So we decided to aggregate simulation metrics per ingame day, before sending it to the client. This lead to design of an entrire module dedicated to metrics.

## Meeting Minutes

### Meeting 1 (Sprint Planning)
Meeting Date 13/11/2024

1. Sprint Goals

.UI Development: Begin implementing the user interface and its connection to backend systems

.API Server: Develop the API server to handle user interactions and integrate with the simulation framework

.Oracle Design: Enhance the advisory system(Oracle) to provide real-time, actionable feedback based on game state.

. Scalability and Game Architecture: Message queue solutions for scalability and real-time game play.
. User Actions and templates for proposed actions.


2. Key Decision Points

 Advisory Systems( Oracle)

Oracle should provide scripted notifications based on predefined thresholds ( e.g., hospital capacity reaching 90%).

Include a menu option where users can request advice based on current game play.

Oracle can be styled as an assistant( e.g., an advisor to a public health official) for better gameplay.

User Interface(UI)
 . A stats page for zooming into specific areas and viewing detailed metrics
 . Visual elements inspired by real-world tools( maps)
 



Simulation Framework

. A way to integrate a compliance server to allow real-time adjustment during simulations.
 
. Discussed using RabbitMQ or similar solutions for scalability.
. Proposed dockerization of the systems for easier deployments.
. Events published to a message queue for real-time UI updates and data storage. 

Game Mechanics and Objectives:
 User should be allowed to face realistic consequences whilst also educating and guiding the user.
 
Types of Action:
 Information dissemination
 Preventative measures (e.g., testings, lockdowns).
 Disease regulations (eg., Vaccination programs).

Next Step
 Finalize the UI prototype and integrate with backend sytems for user testing.
 Implement message queue-based architucture to handle real-time and historical data processing.
 Design and build the Oracle adivosy system with basic functionality for the next sprint review
 Modify compliance and event-driven mechanics in the simulation framework.
 Prepare a structured demo for the customer meeting.

Summary
 The team agreed on key deliverables for next sprint and emphasized importance of addressing scalability and user engagements. 









### Meeting 2
Meeting Date 16/11/2024

Agenda of the meeting

1. Updates and Issues

 . GitHub access rights and merging conflicts.
 . Progress updates on assigned tasks
 . Addressing missing files and repository concerns

2. Sprint Documentation Tasks

 .Assigning roles for meeting notes, user stories and sprint documentation
 .Reviewing user stories and use cases.

3.Clarifications and Next Steps.

 . Task breakdown for the upcoming week
 .Schedule meetings.


Updates and Issues

 Git Issues:
  Problem with merging causing some deletion of files. 

 Plan: Revert to previous commit to recover files.

GitHub Access:
Problems with access resolved.

Task Delegation

 Members within the group decided on working on transferring data from simulation engine to the API service and UI

Implementing a communication protocol (e.g., RabbitMQ) for event handling and commands

Preparing the front end by cleaning up unnecessary elements from the Boilerplate

Prioritizing issues in the GitHub for better visibility of team progress.

Addressing UI rendering issues due to Git conflicts.

Sprint Documentation task

Meeting notes should be  completed.

User stories should be refined using lecture notes to attain consistency.

Use structured templates for clarity in Sprint documents.


Agreed Action plan before next meeting

1) Finalise user stories for Sprint 1 and 2.

2) Resolve repository issues and ensure proper file structure.

3) Complete meeting notes and sprint documentation.

### Customer Meeting and Analysis
Date: 13/11/2024
Attendees: Coral members and Customer

Discussion Points

 1. Simulation Points
  The game simulates the spread of an epidemic using discretized version of the SEIR model and the Wells-Riley equation for infection dynamics.
  Key factors include:
 > Space Characteristics: Volume, ventilation rate, and population density.
 > Agent Behaviour : Probability of infection influenced by other infectious agents in the space.
 > Interventions: The user can impose public health measures, such as Mask mandates, lockdowns and Targeted surveillance. 

2. Demonstration

 2.1 Simulation Setup:

  . Pathogen Properties: Covid-like characteristics with a 7-day incubation period
  . Time resolution: Metrics recorded every 15 minutes but displayed daily
  
  . Metrics Displayed
    .New infections
    .Total active infections
    .Mean Serial interval
  
 2.2 Interactions:
 .Enabling a mask mandate lowered infection rates
 .Lockdown reduced movements but showed more drastic results.

3.Technical Insights

 . The simulation uses a custom-built-agent-based framework.
 .The current setup can simulate 150,000 agents, with scalability planned for millions.




Feedback from the Customer

Target Audience
 Customer asked who the target audience are; Team Coral specified that it include both public health officials and general academics. The game will also ensure accessibility to wilder audiences through gamified learning. 

Simulation Features:
 Customer asked if game can be incorporated to mimic other pathogens? The game have functionality to modify pathogen profiles dynamically( e.g., incubation period, recovery rate, immunity duration).The game also explore ways to simulate broader economic and social impacts, such as GDP changes due to intervention like lockdown.

Oracle Improvements:
 Customer asked how Oracle could be implemented into the game. The game provides actionable advice during interventions, such as when and how to implement specific measures. It also include real-time metrics and projections to enhance user decision-making.

Educational Value:
 The customer and the team agreed that there has to be a balance between a tool for serious learning and potential gamification for broader appeal.

Next Actionable Steps
. Refine and extend the agent-based simulation to incorporate additional pathogens and intervention features
. Resolve technical issues to ensure UI demonstration in the next meeting
. Develop the Oracle feature to include real-time metrics and decision-making support.
. Incorporate feedback loops to enhance educational and gamified aspects.





