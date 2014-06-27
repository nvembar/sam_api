---
layout: default
title: API Basics
nav: basics
---

### API basics

The SAM API is a GET API which has one operation. The operation will retrieve an entity's public information. Its endpoint is ```http://api.data.gov/sam/v1/registrations/```. 

##### Example URL

Currently, the below URL won't work without you adding in an API key from api.data.gov. Add ```?api_key=<YOUR_API_KEY>``` to the below URL to successfully execute the call.

[https://api.data.gov/sam/v1/registrations/1459697830000](https://gw.uat.sam.gov/sam/v1/registrations/1459697830000)

##### Retrieving entity information
The endpoint for getting all data begins with ```/v1/registrations```. 

The endpoint takes a single URL parameter which is the DUNS and DUNS+4 information concatenated. If the entity does not have a DUNS+4, the user should include ```0000```. 

For example, if an entity of interest has a DUNS number of ```012345678``` with no DUNS+4, the access to the endpoint would be at ```/sam/v1/registrations/0123456780000```. An entity with the same DUNS but with a DUNS+4 of ```9999``` would be accessed at ```/sam/v1/registrations/0123456789999```.

##### Finding DUNS numbers to use

Until a search API is implemented (which is on its way), the best way to get DUNS numbers is to go to [SAM](http://www.sam.gov), click on ```Search Records``` and enter in a company into the Quick Search box. Each entity has a DUNS number that you'll see in the result set. You'll see a 9-digit number which represents the DUNS. You can then pad it out with four ```0```s as mentioned above.

##### Coming soon! 

This is just the first of many steps in modernizing SAM and IAE. In fall 2014, SAM API consumers will be able to use the API to search the SAM database and retrieve registration information specific to their needs. This means, most of the functionality you see on SAM right now to search for entities will be available as an API. 

<body id="basics"></body>

