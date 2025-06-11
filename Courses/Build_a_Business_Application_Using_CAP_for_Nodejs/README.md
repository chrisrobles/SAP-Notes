# Build a Business Application Using CAP for Node.js

[Tutorial](https://developers.sap.com/mission.cp-starter-extensions-cap.html)

## Create a Business Service with Node.js Using Visual Studio Code

> Develop a sample business service using Core Data & Services (CDS), Node.js, and SQLite, by using the SAP Cloud Application Programming Model (CAP) and developing on your local environment.

### Prerequisites

#### Node.js

[Install](https://nodejs.org/en/download/)

Run Node.js Shell
`$ docker run -it --rm --entrypoint sh node:22-alpine`

#### SQLite

[Install](https://cap.cloud.sap/docs/get-started/troubleshooting#how-do-i-install-sqlite-on-windows)

Run SQLite
`sqlite3`

#### REST client

[Tutorial](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)

#### Cloud Foundry Trial subaccount

[Tutorial](https://developers.sap.com/tutorials/hcp-create-trial-account.html)

### Tutorial

In Powershell
1. Create project folder
   1. `PS mkdir sap_cds && cd sap_cds`
2. Create Dockerfile
   1. `PS notepad Docker`
   2. Paste in 
    ```text
    # Use the official Node.js image as the base image
    FROM node:22-alpine

    # Install CDS development kit
    RUN npm install -g @sap/cds-dk

    # Set the working directory in the container
    # This is where commands will run out of
    WORKDIR /app
    ```
3. Build the image
   1. `$ docker build -t sap_cds`
4. Run the container with a volume using compose
   1. (optional) Use docker run `$ docker run --name sap_cds -it -v "${PWD}:/app" --rm -p 4004:4004 sap_cds sh`
   2. (recommended) Use docker compose
      1. Create `docker-compose.yaml` next to Dockerfile
      2. Paste in 
         ```yaml
         services:
            sap_cds:
               image: sap_cds
               container_name: sap_cds
               volumes:
                  - .:/app
               ports:
                  - "4004:4004"
               stdin_open: true   # equivalent to -i
               tty: true          # equivalent to -t
               entrypoint: sh     # override the default entrypoint
               restart: "no"      # optional: mimics --rm (compose doesn't auto-remove by default)
         ```
      3. Run `$ docker compose run --service-ports sap_cds`
5. Create CDS project
   1. `$ cds init my-project`
6. Install node packages
   1. `$ cd my-project && npm install`
7. Start a CDS server that updates with changes automatically (except for our case since we are in a docker container)
   1. `$ cds watch`
8. Make data model `db/schema.cds`
    ```cds
    namespace my.bookshop;
    using { Country, managed } from '@sap/cds/common';

    entity Books {
      key ID : Integer;
      title  : localized String;
      author : Association to Authors;
      stock  : Integer;
    }

    entity Authors {
      key ID : Integer;
      name   : String;
      books  : Association to many Books on books.author = $self;
    }

    entity Orders : managed {
      key ID  : UUID;
      book    : Association to Books;
      country : Country;
      amount  : Integer;
    }
    ```
9. Put services with de-normalized views into `srv/cat-service.cds`
    ```cds
    using my.bookshop as my from '../db/schema';

    service CatalogService {
      entity Books @readonly as projection on my.Books;
      entity Authors @readonly as projection on my.Authors;
      entity Orders @insertonly as projection on my.Orders;
    }
    ```
10. Put custom sql table logic in `srv/cat-service.js`
    ```js
    module.exports = (srv) => {

      const {Books} = cds.entities ('my.bookshop')

      // Reduce stock of ordered books
      srv.before ('CREATE', 'Orders', async (req) => {
        const order = req.data
        if (!order.amount || order.amount <= 0)  return req.error (400, 'Order at least 1 book')
        const tx = cds.transaction(req)
        const affectedRows = await tx.run (
          UPDATE (Books)
            .set   ({ stock: {'-=': order.amount}})
            .where ({ stock: {'>=': order.amount},/*and*/ ID: order.book_ID})
        )
        if (affectedRows === 0)  req.error (409, "Sold out, sorry")
      })

      // Add some discount for overstocked books
      srv.after ('READ', 'Books', each => {
        if (each.stock > 111)  each.title += ' -- 11% discount!'
      })
    }
    ```
11. Add initial data
    1. `$ cds add data`
12. Add persistent database
    1. Configure database in `package.json`
        ```json
        {
          "name": "my-bookshop",
          "version": "1.0.0",
          "description": "A simple CAP project.",
          "repository": "<Add your repository here>",
          "license": "UNLICENSED",
          "private": true,
          "dependencies": {
              "@sap/cds": "^7",
              "express": "^4"
          },
          "devDependencies": {
              "@cap-js/sqlite": "^1"
          },
          "scripts": {
              "start": "cds-serve"
          },
          "cds": { "requires": {
              "db": {
                "kind": "sqlite",
                "credentials": { "url": "db/my-bookshop.sqlite" }
              }
          }}
        }
        ```
    2. Deploy SQLite database `$ cds deploy`


## Deploy a CAP Business Application to SAP Business Technology Platform

> This tutorial shows you how to deploy your SAP Cloud Application Programming Model (CAP) application to SAP Business Technology Platform (BTP), Cloud Foundry environment using SAP HANA Cloud service.

### Prerequisites

#### CF Command Line Client

Install the Cloud Foundry Command Line Interface

[Tutorial](https://developers.sap.com/tutorials/cp-cf-download-cli.html)

#### MBT Built Tool

[Tutorial](https://sap.github.io/cloud-mta-build-tool/download/)

#### MultiApps CF CLI Plugin

[Download](https://github.com/cloudfoundry/multiapps-cli-plugin/blob/master/README.md)

> MultiApps Controller is based on the Multitarget Application (MTA) model and enables operating CF entities with a single command, while ensuring consistency and completeness of the entire MTA.
> > MTA is where CF apps are modeled as modules and services as resources. MTA model enables the delivery of packaged apps, where any target specific configuration could be specified on deployment time without changing application code.

#### SAP HANA Cloud Instance

[Tutorial](https://developers.sap.com/tutorials/hana-cloud-mission-trial-3.html)

[Deploy tutorial](https://developers.sap.com/tutorials/hana-cloud-deploying.html)