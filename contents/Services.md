<h1>API: Services</h1>

Make sure to read the API Introduction before this document.

<h2>Retrieving A Service List</h2>

<h3>Required Variables</h3>

* section must be set to services .
* action must be set to retrieve .
* api_key must be set to [your unique API key](../README.md#finding).

<h3>Optional Variables</h3>

* service_id - an integer or set of integers specifying the set of service IDs you would like us to list. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all services. This parameter is set to all by default.

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and service information.
