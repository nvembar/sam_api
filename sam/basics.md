---
layout: default
title: API Basics
nav: basics
---

### API basics

The SAM API is a GET API which has one operation. The operation will retrieve an entity's public information. It's endpoint is ```http://gw.uat.sam.gov/SamStatus/registrations/```. Note that this endpoint is currently pointing to the SAM UAT environment and will be updated when the API goes into production.

##### Example URL

[https://gw.uat.sam.gov/SamStatus/registrations/1459697830000](https://gw.uat.sam.gov/SamStatus/registrations/1459697830000)

##### Retrieving entity information
The endpoint for getting all data begins with ```/registrations```. 

The endpoint takes a single URL parameter which is the DUNS and DUNS+4 information concatenated. If the entity does not have a DUNS+4, the user should include ```0000```. 

For example, if an entity of interest has a DUNS number of ```012345678``` with no DUNS+4, the access to the endpoint would be at ```/SamStatus/registrations/0123456780000```. An entity with the same DUNS but with a DUNS+4 of ```9999``` would be accessed at ```/SamStatus/registrations/0123456789999```.

<body id="basics"></body>
