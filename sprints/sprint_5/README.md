# Sprint 5: 2024-11-27 to 2024-12-03

## Overview

## Review

## Meeting Minutes

### Meeting 1

### Meeting 2

## Backlog

### Complete Backlog Tasks

### New Backlog Tasks

## Exception Handling

## Product Documents

### Customer Meeting and Analysis
Customer meeting 5
Date: 27/11/2024
Attendees: Customer and Team Coral




 1. Sprint Goals:



• Share progress on the game project.

• Discuss challenges related to data accuracy and performance.

• Identify the next steps for front-end and back-end integration.



2. Key Discussion Points:



A. General Updates:



• Project Purpose:

The primary objective of the meeting was to showcase the progress made in game mechanics, including a functional UI.

• Progress Achievements:

• Successfully integrated data from the Office for National Statistics (ONS) for population density.

• Focused on London’s data for initial implementation.

• UI improvements are in progress.



B. Technical Details:



1. Data Integration:

• Utilized ONS census data to determine population densities and local authority districts (LADs).

• Implementation goes as fine-grained as output areas but avoids individual postcodes for efficiency.

2. Population Density and Space Allocation:

• Spaces (residences, offices, social areas) are allocated based on population density:

• More dense areas → More spaces.

• Less dense areas → Fewer spaces.

• Plans to aggregate metrics at LAD and Middle Layer Super Output Area (MSOA) levels.

3. Simulation Challenges:

• Current Issues:

• Running simulations with 1 million agents causes delays (8 seconds for a game day).

• Computational load is significant, especially for large populations.

• Proposed Solutions:

• Adjusting the simulation time step (from 15 minutes to 1 hour) to reduce load.

• Optimizing simulations for high-performance environments or cloud services.

• Introducing representative agents (one agent representing multiple people).



3. Architecture Overview:



• Simulation Service:

• Separate from the front end.

• Can be run on high-performance servers or laptops, depending on the user’s resources.

• Designed for scalability and university-level usage.

• Front-End/Back-End Integration:

• Current Status:

• Core back-end functionalities are in place.

• Front-end integration is ongoing.

• Next Steps:

• Complete integration to allow user actions in the UI.

• Focus on making the UI more interactive in the next sprint.



4. Challenges and Action Items:



1. Challenges Identified:

• Scalability and performance optimization.

• Ensuring accurate simulations while reducing computational load.

• UI and back-end communication delays due to mapping tasks.

2. Action Items for the Next Sprint:

• UI Focus:

Complete integration of user actions into the front end.

• Optimization:

Explore cloud deployment and representative agent strategies.

• Testing:

Conduct small-group tests for potential deployment options.

• Documentation:

Improve internal documentation to streamline development processes.



5. Next Steps and Review Plan:



• Short-Term:

• Focus on UI interactivity and system optimization.

• Address scalability issues with high-density simulations.

• Long-Term:

• Continue testing and refining simulations.

• Document progress thoroughly to enhance team collaboration.

• Next Review:

[Insert Date] (one week from this meeting).



Meeting Conclusion:



• The team acknowledged current challenges and outlined clear steps to address them.

• Progress will be reviewed in the next sprint, focusing on integration, testing, and optimization.



### User Stories

[goto user stories](https://github.com/CoralCoralCoralCoral/documentation/blob/Use-Cases/sprints/sprint_5/user_stories.md)


### User Cases

[goto user stories](https://github.com/CoralCoralCoralCoral/documentation/blob/Use-Cases/sprints/sprint_5/use_cases.md)

#### Summary of Changes
