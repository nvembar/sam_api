---
published: true
layout: default

---

As part of the next SAM quarterly release, the SAM API service will expand to include the functionality for Search.  The SAM Search API has been developed to mimic the Search functionality that is currently available from the SAM website.  
The Search API provides the opportunity to perform a search transaction in the following two options. Quick Search which takes a single search term provided by the user and compares it to a set of predefined database fields.  Advanced Search allows the user to search by entering a value that is then used to search a user selected predefined search category. 

### Searching SAM using the API

#### Quick Search:

The Quick Search functionality allows a user to enter a single term which is then queried against eight fields in the SAM database.  The results should return the same businesses, grantees, and other registrants in SAM that are found when you do a "Quick Search" 

Example: [https://api.data.gov/sam/v1/registrations?qterms=GSA](https://api.data.gov/sam/v1/registrations?qterms=GSA)

You can include spaces by putting them in double-quotes and URL-encoding them like so:

[https://api.data.gov/sam/v1/registrations?qterms="My%20Company](https://api.data.gov/sam/v1/registrations?qterms="My%20Company")

The Search API will then query the SAM database and display any registrant that matches the user selected search term contained in any of the following fields: 

| Field                  |
|------------------------|
| Legal Business Name    |
| Doing-Business-As Name |
| DUNS                   |
| DUNS+4                 |
| CAGE Code              |
| DoDAAC                 |
