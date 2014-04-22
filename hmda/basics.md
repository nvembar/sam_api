---
layout: default
title: API Basics
nav: basics
---

### API basics

The SAM API is a GET API which has one operation. The operation will retrieve an entity's public information. It's endpoint is [http://gw.uat.sam.gov/SamStatus/registrations/](http://gw.uat.sam.gov/SamStatus/registrations/). Note that this endpoint is currently pointing to the SAM UAT environment and will be updated when the API goes into production.

##### Retrieving entity information
The endpoint for getting all data begins with ```/registrations```. 

The endpoint takes a single URL parameter which is the DUNS and DUNS+4 information concatenated. If the entity does not have a DUNS+4, the user should include ```0000```. 

##### Concepts
Concepts are analogous to variables, or column headers in a spreadsheet. Concepts have properties, which describe all the possible values. You can also specify concepts in any of the supported file formats like so: ```/data/{dataset-name}/{contept-name.extension}```. 

<a href="console/#!/hmda/getConceptHmda_get_1" class="action-arrow">Try it out <i class="icon-right"> </i></a>

<body id="basics"></body>
