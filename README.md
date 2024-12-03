# Golding Frontend Application

This is a brief documentation of the Golding Backend application, you can get the detailed pdf documentation of the project from the email i sent as regards to this project.

## Frontend Application Setup:

1.	Make sure that you have node install in the environment you want to run the application, you can download and install the latest stable version of node at this location. https://nodejs.org/en/download/prebuilt-installer
2.	You can clone the frontend application from this git repository: https://github.com/tacheons/golding_frontend.git
3.	Run the following command to install the dependencies npm i
4.	Run npm run dev to start up the application
5.	The application will be available at this url on port 3000, http://localhost:3000


## Frontend Architectural Diagram
This is the detailed schematics of the frontend system using Model-View-View-Model (MVVM) Architecture. MVVM Model like Vue.js or React.js is a reactive system that intercepts user requests and handles all it views via a Single Page Application (SPA) by pre-computing and manipulation of the DOM to generate the expected views without sending further requests to the server. It can make remote calls to the remote server to fetch only data that it can render, unlike Server Side Rendering (SSR). That end the entire page from the server

                                          
![mvvm](https://github.com/user-attachments/assets/63765aca-2063-47d6-9393-34abd3d61ce4)

## Component Structure:
This is the schematics on how the components stacks up on the frontend application.
                                          
![components_structure](https://github.com/user-attachments/assets/d7b79939-62b8-4185-8aad-491d35c6d994)

## Choice of Tech Stacks:
Base on the requirement analysis, the type of system to be developed, the Domain Driven Design (DDD) and the possible user metric, as regard to level of usage and interaction, the design structure and the tech stack can be determined.
Below is my choice of tech stack base on my analysis and the information I have gotten so far on the application.

## Frontend Tech Stack:
I implement the architecture on vue.js framework, with following technologies;
1.	JavaScript 
2.	HTML
3.	CSS
4.	Bootstrap UI
5.	NPM Packages
Alternative framework will be React.js or Svelte

