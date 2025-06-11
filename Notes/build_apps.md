# Build Apps

SAP Build Apps
- Low/no code application development tool

Must run on a custom identity provider user from the Cloud Identity Services (the part of BTP that defines all the users)

[Install (see Step 2)](https://developers.sap.com/tutorials/codejam-0-prerequisites.html#76cc6857-c70a-4e56-a03a-41e6043a67fe)

## Project Types

Objective > Category > Type
- Application: create business apps and services
  - Full-Stack: Full-stack application (frontend and backend)
    - Full-Stack ABAP: based on ABAP cloud development model
    - Full-Stack Node.JS: based on SAP Cloud Application Programming Model (CAP) for the backend and SAP Fiori and MDK for frontend
    - Full-Stack Java: based on SAP Cloud Application Programming Model (CAP) for backend and SAP Fiori for the frontend
  - Frontend: web UIs
    - Web & Mobile Application: web and mobile applications that connect to your SAP or 3rd party data
    - SAP Fiori: build UI for existing back-end service, using freestyle SAPUI5 or SAP Fiori elements
  - Backend: server-side applications
    - Application Backend: data models and backend logic for existing web / mobile application
  - Mobile: iOS and Android apps in the cloud
- Automated Process: automate processes and tasks
- Business Site: create business sites

## App builder Area

Build an app using the app builder area

[Features](https://help.sap.com/docs/build-apps/service-guide/what-is-sap-build-apps)

### User Interface

#### Properties

- Change text in Properties > Content (useful for formula or variable based text)
- Binding type (data type) on input and output can be changed between things such as Static value, Data and variables, formula, component properties, output value of another node (output of a node up the path), and Mapping

#### Logic Canvas

Event and actions (flow functions)

Input and Output
- Input received through the connection
- Output can go through several ports depending on what happened
  - Output tab (next to properties tab) shows what each port does

Event
- Component tap: user clicks something

### Variables

5 types of variables
- App variables: written and read by any page
- Page variables: written and ready by a page
- Page parameters: read-only passed to the page on navigation
- Data variables: used by current page
- Translation variables: text values translated according to current language of the user

- Default set variable on page load

### Integrations

#### On-device storage

#### Integrations

#### SAP Build Apps classic data entities

Universal REST API integration
- "Autodetect Schema from Response" after testing API call to store the data structure

Connect to REST API

OData integration

SAP BTP Destination REST API integration

Google Firebase / Cloud Firestore

Marketplace search

Google Firebase