# myntech-io-utils-securityissues
An Api service through which you can find software security issues presents in Nist CVE/CPE databases

**Tech Specs**
- .Net 5.0
- WebApi
- Swagger
- Basic Auth (to be replaced with the auth system you need)

**Basic Auth**

All the endpoints requests needs to be authorized with a BasicAuth login and password (myntech/myntech_01)

**Swagger**

The service follows the OpenApi specs, so the default endpoint for test purpose is /swagger (you can disable it for production environments)

**Nist Documentation**

The service has been developed following the specs indicated by Nist at these Urls:

CVE
https://csrc.nist.gov/CSRC/media/Projects/National-Vulnerability-Database/documents/web%20service%20documentation/Automation%20Support%20for%20CVE%20Retrieval.pdf

CPE
https://csrc.nist.gov/CSRC/media/Projects/National-Vulnerability-Database/documents/web%20service%20documentation/Automation%20Support%20for%20CPE%20Retrieval.pdf

**How to use it**

- At the moment there are 2 endpoints:
-   securityissues/cve
-   securityissues/cpe

Both the endpoints must be called with:
- BasicAuth in place
- NistCveRequestModel or NistCpeRequestModel as json body value

The request models you pass in the request body performs the filtering actions on the Nist relative endpoint.
So, for example, if you fill in the value for "keyword", it will add the "keyword" parameter to the Nist endpoint.
If no parameters will be passed, it sends a request to the Nist endpoint and you'll receive back the last 20 results.

**Models**

In the specific folder of the project you'll find the models that maps the Nist response
All the responses generated by our service are wrapped inside an ApiResponseModel, that contains the following elements:
- Payload --> when everything is ok it contains the Nist response, mapped to the NistCveResponseModel or NistCpeResponseModel
- Status --> two self-explanatory values: OK or KO
- Message --> it will be filled in with the excepetion message; this happens when there is an exception and the Status will be also passed to KO

**Helpers**

In this folder there are 2 classes:
- ApiCaller.cs --> it performs the requests to the Nist endpoints
- BasicAuthenticationHandler.cs --> it performs the Auth process and here you'll find also the username and password used for the authentication (if you want to replace it)
