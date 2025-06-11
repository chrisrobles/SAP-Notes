# Core Data Services

> Data modeling framework used to define and consume semantic data models with database design in mind

i.e. used to define views and models on top of database tables using SQL-base syntax

`cds init my_project`

## files

### app

for ui

### db

database level schema model

normalized entity definitions

ex. `schema.cds`
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

### srv

for the service definition layer

services expose potentially de-normalized views on those entities

ex. `cat-service.cds`
```cds
using my.bookshop as my from '../db/schema';

service CatalogService {
  entity Books @readonly as projection on my.Books;
  entity Authors @readonly as projection on my.Authors;
  entity Orders @insertonly as projection on my.Orders;
}
```

### package.json

## commands

`cds watch` starts a cds server and automatically updates with changes
- `--watch-mode=poll` sets the update to consistently check for changes rather than relying on inotify which doesnt always update when the volume updates since the changes are happening on local (depends on version if this is supported)

`cds add data`

Add plain csv files (just the headers) for all entities in `db/data/`

`cds add`

- `--for production` adds all configuration added by this command in the package.json file into a cds.requires.[production] block.

- ``hana` configures deployment for SAP HANA, so a data source of type hana is added in the cds.requires.[production].db block. See section [Node.js configuration](https://cap.cloud.sap/docs/node.js/cds-env#profiles) in the CAP documentation for more details.

- ``mta` adds the mta.yaml file. This file reflects your project configuration.

- ``xsuaa` creates an xs-security.json and also the needed configuration in the mta.yaml file. An authentication of kind xsuaa is added in the cds.requires.[production].auth block.

- ``approuter` adds the configuration and needed files for a standalone AppRouter so that the authentication flow works after deployment.
