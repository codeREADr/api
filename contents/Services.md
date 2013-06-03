<h1>API: Services</h1>

Make sure to read the API Introduction before this document.

<h2>Retrieving A Service List</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b> .
* <b>action</b> must be set to <b>retrieve</b> .
* <b>api_key</b> must be set to [your unique API key] [1].

<h3>Optional Variables</h3>

* <b>service_id</b> - an integer or set of integers specifying the set of service IDs you would like us to list. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all services. This parameter is set to all by default.

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and service information.

Example :

```xml    
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <service id="120">
        <name>Friday event</name>
        <validationmethod>postback</validationmethod>
        <postback>https://www.postbackurl.com</postback>
        <user id="123"/>
        <user id="124"/>
        <question id="480"/>
    </service>
    <service id="380">
        <name>Boston Marathon</name>
        <validationmethod>database</validationmethod>
        <database>757</database>
        <duplicateScanValue>1</duplicateScanValue>
        <user id="124"/>
        <user id="125"/>
        <question id="482"/>
        <question id="484"/>
    </service>
</xml>
```

<h2>Creating a Service</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b> .
* <b>action</b> must be set to <b>create</b> .
* <b>api_key</b> must be set to [your unique API key] [1] .
* validation_method - an enum type that specifies the service type you desire for your new service. You must set it to one of these options:
    * <b>record</b> (Record Scans Online)
    * <b>ondevicerecord</b> (Record Scans On-Device)
    * <b>database</b> (Validate Scans Online)
    * <b>ondevicedatabase</b> (Validate Scans On-Device)
    * <b>postback</b> ([Postback URL](Postback.md#head))

If <b>validation_method</b> is set to <b>database</b> or <b>ondevicedatabase</b> :

* <b>database_id</b> - a string which must be included and set to the ID of the database the scans will be validated against.

If <b>validation_method</b> is set to <b>postback</b> :

* <b>postback_url</b> - a string which must be included and set to the destination URL where all scans will be forwarded to. (More info.)

<h3>Optional Variables</h3>

[1]:../README.md#finding
