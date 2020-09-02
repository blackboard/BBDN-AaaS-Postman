# BBDN-AaaS-Postman

This repository contains a postman collection for testing the Ally as a Service REST APIs. In order to use this repository, you will need a Client ID, key, and secret. For more information on this API and how to obtain the key and secret, visit the [Blackboard Developer Community](https://docs.blackboard.com/ally).

## Usage
To use this repository, you must have Postman installed. From the UI, click the import button and follow the on-screen prompts. The collection is already configured to use https://ally.prod.ac as the top-level domain.

The easiest way to use this collection is to have Postman generate the JWT token for each request. To do this:

1. Execute INIT: Load Crypto Library for HS256 to load the library into your postman globals
2. Update the collection variables with the following:
   * ALLY_CLIENT_ID - Your Collaborate REST API Key
   * JWT_secret - Your Collaborate REST API Key
3. Execute Ally requests

The Pre-Request script will generate a JWT token for use during each request. You should call the `Upload a file to Ally` endpoint first, as this generates a contentHash that the other requests require to operate. In the body of this request, you will need to click the button next to 'file' and select a file for processing before clicking send. On successful completion, the collection will automatically parse out the contentHash and set to an environment variable, which the other endpoints are already configured to use as appropriate.

To `Check the processing status of a file`, you may simply click Send. This is all configured via environment variables.

Finally, to `Retrieve the feedback for a file`, you will need to check the _Params_ tab of the request. Here there is a _feedback_ parameter, which may be set to `true`, `false`, or omitted. Setting to true will retrieve the full report. Setting to false or omitting this value will return only the metadata of the report. To test omission, simply uncheck the box next to feedback.
