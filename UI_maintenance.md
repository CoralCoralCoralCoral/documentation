### UI Maintenance Guide

## File Structure Overview

app - contains the different pages, layout doc, global css doc and the fonts used.
api - handlers for server-side logic and API routes.
components\ui - reuseable UI components.
hooks - custom react hooks.
node_modules - directory containing installed dependencies managed by npm or yarn. This folder is auto-generated and should not be modified manually.
store - contains the different slices of store along with the respecitve reducers. 

## Dependencies Management

Regularly update dependencies using npm outdated or yarn outdated.

Remove unused dependencies.

Test thoroughly after updates to avoid breaking changes.

## Build and Deployment

Use next build for optimized builds.
