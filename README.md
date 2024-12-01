# Golding Frontend Application

This is a brief documentation of the Golding Backend application, you can get the detailed pdf documentation of the project from the email i sent as regards to this project.

## Steps to run this project:

1. clone the repository here `https://github.com/tacheons/golding_frontend.git`
2. Run `npm i` command
3. Run `npm run dev` command

## Frontend Architectural Diagram
This is the detailed schematics of the frontend system using Model-View-View-Model (MVVM) Architecture. MVVM Model like Vue.js or React.js is a reactive system that intercepts user requests and handles all it views via a Single Page Application (SPA) by pre-computing and manipulation of the DOM to generate the expected views without sending further requests to the server. It can make remote calls to the remote server to fetch only data that it can render, unlike Server Side Rendering (SSR). That end the entire page from the server

![mvvm](https://github.com/user-attachments/assets/6b5e51df-164c-4556-ae94-abebfa4ea220)

## Component Structure:
This is the schematics on how the components stacks up on the frontend application.

![components_structure](https://github.com/user-attachments/assets/7d2fe000-5a6c-457f-b70e-2f5e3a4f98ea)

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

