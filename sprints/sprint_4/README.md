# Sprint 4: 2024-11-20 to 2024-11-26

## Sprint Goal

## Sprint Overview

## Sprint Review

## Exception Handling


## Meeting Minutes

### Meeting 1 (Sprint Planning)
Date: 20/11/2024
Attendees: Team Coral

Key Discussion Points
 Need to do detailed documentation of retrospective meetings

 Prioritation of sprint documentation

 Ensure all documentations are cohesive and ready for assessments

 Define clear acceptance cretaria for each user story

Link user stories to corresponding use cases

ensure each user stories include multiple use cases to illustrate different scenarios

Clarify the states of each task at the end of the sprint

Review user stories and ensure all taks have defined owners and states.

Action Plan for next sprint

Establish a consistent format for sprint documentation

ensure ongoing task are properly documented and tracked.



### Meeting 2
Place: Teams 
Date: 23/11/2024
Attendees: Team Coral 

Agenda

1) Review of Oracle use cases

2) State Transition Modelling

3)  UI and Provinces Data Model

4) Front-End and Backend integration

5) Deployment Repository and Build Processes


1. Review of Oracle Use cases

 Purpose:
  
 Design oracle use cases to notify users about critical threshold and provide actionable advice.

Eg., When hospital capacity exceeds 90%, the Oracle;

Pause the game
Informs the user of the situation and suggests a lockdown
Offer additional details or alternative actions.



2) State Transition Modelling
 .Current states: Not Infected, infected, ill, dead.
 .Proposed additional states: Hospitalized, Deceased

 Discussion Points
 .Introduce variable stochastic probabilities for hospitalization and recovery time based on agent's health state
 . Model healthcare workers as a separate category.
 .  Hospitals as potential infection spread hubs, especially during early outbreaks.

3) UI and Provinces Data Model
 A sidebar to display available actions with future plans to add localized actions.

 Development underway to introduce a structure for jurisdictions

 Simplified dropdown implementation for initial testing


4) Frontend and backend integration

 Successfully displaying UI on servers

 Progress on web socket integration for message transmission between frontend and backend.


5) Deployment Repository and Build processes

 Current method involves manual build and development of the front end.

 Proposal to automate the build process using GitHub actions and integrate it into the deployment repository

 Set up a deployment repository for modularity

 Exclude build versions of the UI from the API server repo.


Next Step
. continue refining Oracle use cases and state transitions

. Finalize provinces data model and actions UI

.Integrate automation for front-end deployment

.Prepare healthcare worker modelling for next sprint.

### Customer Meeting and Analysis
Customer meeting 4

Date:20/11/2024
Attendees: Customer and Team Coral

Agenda

1) UI Development Status

2) Simulation Infrastructure and Data Processing

3) Next Sprint Goals

4) Customer Feedback and Clarification

5) Discussion on Oracle Implementation


Meeting Summary

1. Current Progress

 UI Progress:
 .Interactive map framework completed but does not yet display simulation data.
 .Planned functionality includes displaying infection statistics by location and enabling historical searches.

.Backend Infrastructure:
 . Developed infrastructure for simulation event handling, including:
  .Message Queues: For efficient communication between UI and Simulation.
  .Elastic Search: For indexing simulation data to facilitate historical searches via REST API.

.Concrete User Actions:
 .Established a list of actionable user interactions for implementation in the next sprint.

2. Customer Feedbacks
 1. Functionality expectations:
    . Focus on achieving core functionality before expanding features
    . Deliver a fully playable system with clear start, middle and end.
 
 2. Custom Scenarios
    .Current focus on predefined scenarios is acceptable
    . Highlight in documentation how the system can be extended for custom scenarios in the future

 3. Documentation Suggestions:
    . Include modular design consideration to demonstrate potential tweak for future enhancements
    . Document unimplemented features as potential improvements.
 4. Oracle Design
    . The oracle should assist without making them too reliant.
    .Consider a scalable Oracle model, potentially adaptable based on user experience levels.


Challenges and Concerns
 Concern about delivering the perfect game was raised. Customer wants the team to prioritize playability and core functionality over perfection.
 Frontend-backend connection not complete. Customer wants integration.


Action Plan for Next Sprint
 1. UI Integration
 2. Implement user actions  for interacting wit the game
 3. Develop a reactive Oracle to provide contextual advice based on game states.
 4. Ensure the Oracle system is modular and extendable for future refinements.
 5. Test and debug the core gameplay loop to ensure stability and usability. 
