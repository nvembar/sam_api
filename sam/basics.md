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

##### Finding DUNS numbers to use

Until a search API is implemented (which is on its way), the best way to get DUNS numbers is to go to [SAM](http://www.sam.gov), click on ```Search Records``` and enter in a company into the Quick Search box. Each entity has a DUNS number that you'll see in the result set. You'll see a 9-digit number which represents the DUNS. You can then pad it out with four ```0```s as mentioned above.

<body id="basics"></body>
