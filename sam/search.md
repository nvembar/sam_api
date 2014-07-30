---
published: true
layout: default

---

*NOTE: All the documentation on this page refers to the October release of the API*

As part of the next SAM quarterly release, the SAM API service will expand to include the functionality for Search. The SAM Search API has been developed to mimic the Search functionality that is currently available from the SAM website.
The Search API provides the opportunity to perform a search transaction in the following two options. Quick Search takes a single search term provided by the user and compares it to a set of predefined database fields. Advanced Search allows the user to search by entering a value that is then used to search a user selected predefined search category. 
Notice that we are implementing this through a JSON-based “hypermedia as the engine of application state” (HATEOAS with the appropriate links object within the result set). The intent going forward will be to use this model to allow for a scalable architecture of IAE’s APIs to be built. 
Note:  Don’t try to construct links yourself based on the patterns you see in the links object. Assume that those patterns could change. We will account for this requirement as we implement our rate-limiting for the API.
Searching SAM using the API
Quick Search:
The Quick Search functionality allows a user to enter a single term which is then queried against six fields in the SAM database. The results should return the same entities, grantees, and other registrants in SAM that are found when you do a “Quick Search” on SAM itself.
Example: https://api.data.gov/samsearch/v1/registrations?qterms=GSA
The Search API will then query the SAM database and display any registrant that matches the user selected search term contained in any of the following fields: 

Field
Legal Business Name
Doing-Business-As Name
DUNS
DUNS+4
CAGE Code
DoDAAC


Note that the search will automatically add a wildcard to the end of any term passed in quick search. So qterms=Rob will match “Robot Co., Inc.”
Advanced Search:
The Advanced Search functionality allows a user to enter criteria or a value and a category which is then used to query the database to return all registrations that match that selection criterion. In Advanced Search users are able to string multiple criteria and categories to better refine their search and return a more specific list of registrations.
Advanced Search uses the same qterms construct that we used for quick search, but follows more closely to the Lucene-based syntax for querying by specific terms. It is not exactly the same, but should be familiar for anyone who is used to that syntax.
As a basic example, if you want to make sure you’re searching only Legal Business Name, you can run the following search:
https://api.data.gov/samsearch/v1/registrations?qterms=(legalBusinessName:incorporated)
The search terms will be in parentheses. You can group AND and OR search terms together by putting the terms AND or OR between terms, separated by spaces. (Eventually, they will be separated by + signs because of some ambiguities in the syntax, but for the moment, use spaces.)
For example a user can search for an entity that has a Legal Business Name that includes the term “incorporated” AND has selected the NAICS Code of 123456 for which they are considered to be a Small Business for. 
https://api.data.gov/samsearch/v1/registrations?qterms=(legalBusinessName:incorporated) AND (naicsLimitedSB:12345)
Advanced search fields
The following are the fields you can search for using Advanced Search. Note that, where appropriate, we have used the same field name as the JSON output from the detailed results of the API. Some of them, like minorityOwned are interpreted appropriately.

TABLE

Codes for Purpose of Registration
•	Z1 - Federal AssistanceAwards (Grantees)
•	Z2 - All Awards (Contracts and Federal Assistance)
•	Z4 - AssistanceAwards & IGT
•	Z5 - All Awards & IGT
Codes for Registration Status
•	A - Active
•	W - Work in Progress
•	S - Submitted
•	I – Inactive
API Search Output:

The search results that match the searched condition will be displayed in JSON format and include the following data elements:

TABLE

The JSON result will return as follows:
{"results":[{"hasKnownExclusion":false,"samAddress":{"zip":"12345","zip4":"3800","stateOrProvince":"IL","line1":"1234 M St","city":
"Chicago","country":"USA"},"expirationDate":"2015-03-24 13:56:45.000",
"status":"Active","hasDelinquentFederalDebt":false,"duns":"123456789","links":[{"rel":"details","href":"http://api.data.gov/samdata/v1/registrations/1234567890000"}],"dunsPlus4":"0000","legalBusinessName":"Sample Company LLC","cage":"12345"}],"links":[{"rel":"self","href":
"http://api.data.gov/samsearch/v1/registrations?qterms=123456789&start=1&length=10"}]}

Pagination

The results will be defaulted to 10 records per JSON page. An API developer can navigate between pages by using the Self, Previous, First, and Next links (as appropriate depending on the number of records) at the end of each page.

"links":[{"rel":"self","href":"http://api.data.gov/samsearch/v1/registrations?qterms=gsa&start=11&length=10"},{"rel":"prev","href":"http://api.data.gov/samsearch/v1/registrations?qterms=gsa&start=1&length=10"},{"rel":"first","href":"http://api.data.gov/samsearch/v1/registrations?qterms=gsa&start=1&length=10"},{"rel":"next","href":"http://api.data.gov/samsearch/v1/registrations?qterms=gsa&start=21&length=10"}

An API developer can change the number of records returned per page by manipulating the start and length parameters at the end of the API search URL like so:

http://api.data.gov/samsearch/v1/registrations?qterms=gsa&start=1&length=25

Connecting Search Fields

Plus signs '+’ should be used as spaces between terms. ‘+AND+’ and ‘+OR+’ are always used to join two terms like a boolean AND and OR.

https://api.data.gov/samsearch/v1/registrations?qterms=legalBusinessName:University+of+Pongo

https://api.data.gov/samsearch/v1/registrations?qterms=disasterResponse:true+AND+samAddress.stateOrProvince:CO

https://api.data.gov/samsearch/v1/registrations?qterms=naicsAnySize:111411+AND+samAddress.stateOrProvince:XY+AND+legalBusinessName:Test+AND+minorityOwned:true

If your search term contains the word(s) ‘and’ or ‘or’, you must not capitalize it.

Example:
https://api.data.gov/samsearch/v1/registrations?qterms=legalBusinessName:Snow or Sleet Removal Company 

https://api.data.gov/samsearch/v1/registrations?qterms=legalBusinessName:Rain or Shine Rentals 

Grouping Search Terms

Terms can be grouped against the same API advanced search field by using commas between each term.

Examples:
https://api.data.gov/samsearch/v1/registrations?qterms=samAddress.zip:(11111,22222,33333)

https://api.data.gov/samsearch/v1/registrations?qterms=congressionalDistrict:(AK-00,AS-98,AZ-06)

https://test.sam.gov/samsearch/v1/registrations?qterms=womanOwned:true+AND+naicsLimitedSB:(111333,111991,111331)

Note: For terms having the first character as alpha, you must insert a + symbol after each comma (exception is samAddress.country).

Examples:
https://test.sam.gov/samsearch/v1/registrations?qterms=legalBusinessName:(wood,+moore,+general,+temme,+whitney)

https://test.sam.gov/samsearch/v1/registrations?qterms=samAddress.city:(Moscow,+Oslo,+Geneva)

https://test.sam.gov/samsearch/v1/registrations?qterms=naicsAnySize:(111332,336413)+AND+samAddress.city:(Napa,+Loire)

Exception: https://test.sam.gov/samsearch/v1/registrations?qterms=samAddress.country:(ALB,BLZ,CHL)


TIPS/HINTS

There are certain tips to note in order to construct an API search URL properly. We have listed several below. If you discover others as you work with our API, please add them to the ‘Feedback’ section of this GitHub site.

1. Any query terms with special characters must include double quotes: q= “ZY’Z”
	Note:  %26 can be used for ampersand ‘&’

2. Commas must be omitted from search terms

3. Boolean based search fields must be grouped together at the front of a URL:
Note: If your search includes ‘Disaster Response Contractor, the disasterResponse search field must be the last Boolean search field in the group
Example: qterms=womanOwnedBusiness:true+AND+sba8AProgram:
true+AND+disasterResponse:true+AND+legalBusinessName:cats

4. There should only be one space (‘+’) between each term and in between “AND” and “OR”
5. Quick Search does not allow grouping

6. When grouping Legal Business Name and Country in an advanced search, the term legalBusinessName must come before samAddress.country.

Example:
https://test.sam.gov/samsearch/v1/registrations?qterms=legalBusinessName:technology+OR+samAddress.country:XYZ
