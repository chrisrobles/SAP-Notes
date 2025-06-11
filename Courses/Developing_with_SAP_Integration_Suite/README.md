# Developing with SAP Integration Suite

[Source](https://learning.sap.com/learning-journeys/developing-with-sap-integration-suite)
[SAP BTP Trial Link](https://account.hanatrial.ondemand.com/trial/#/home/trial)


SAP Integration Suite provides the ability to design, develop, and operate **APIs**.

## Prerequisites

1. Need one of the following:
- [SAP BTP trial account](https://community.sap.com/t5/technology-blogs-by-members/sap-btp-trial-account-creation-and-enabling-integration-suite-service-sap/ba-p/13702052)
- Free tier model for SAP BTP
- Enterprise SAP BTP account
1. Provision subaccount with the SAP Integration Suite
2. Activate
   1. API Management
   2. Cloud Integration
3. Assign role collections to the appropriate user

## Introduction

> Distributed IT System
> > Comprises subsystems (components in the broadest sense) that are coupled together within the framework of a specific architecture and handle tasks cooperatively.

> Monolithic IT System
> > Functions of a system are bundled (centralized). The logical distribution of system functions among components can be accompanied by a coordinated physical decentralization in a computer network.

Due to differences between systems, challenges arise such as:
- diverse transport protocols
- security
- latency
- monitoring

One solution is **API First Approach**

### API First Approach

Primary focus during the development process is the application programming interface (API).

Services are interfaced with by APIs. APIs have different implementations, but they are all language agnostic (not dependent on the programming language). 

Key Aspects of an API-first approach include:
1. **Design-Centric**: Prioritizes clarity, consistency, and usability to ensure developers have no troubles with the API.
2. **Iterative Development**: Iterates on the API using feedback before moving on to the rest of the application
3. **Facilitates Collaboration**: Allows different development teams to work in sync and reduce dependencies
4. **Ensures Scalability and Flexibility**: Promotes modular components making scaling and future changes easy
5. **Focus on Developer Experience (DX)**: Provides developers with documentation, SDKs (Software Development Kits), code samples, and testing tools to ease setup and usage of the API.
6. **Supports Ecosystems Growth**: Fosters an ecosystem around the API that allows for third-party collaboration.

## Services

### Integration Solution Advisory Methodology | ISA-M

Design solution architecture with the tools and concepts of the SAP Integration Suite

### Cloud Integration

Request is sent and iFlow is started

### API Management

Encapsulates the API of the database

### ES5 Database

The database

### SAP Cloud Identity Service

Authorization