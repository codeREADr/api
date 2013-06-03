<a name="head"></a><h1>API: Services</h1>

Make sure to read the API Introduction before this document.

<a name="retrieve"></a><h2>Retrieving A Service List</h2>

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

<a name="create"></a><h2>Creating a Service</h2>
<a href="#head">Back to top</a>

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

* <b>postback_url</b> - a string which must be included and set to the destination URL where all scans will be forwarded to. ([More info.](Postback.md#head))

<h3>Optional Variables</h3>

* <b>service_name</b> - a string which specifies the desired name of your new service. The default is "Service $i", where $i is the next available sequential number.
* <b>description</b> - a string which specifies the desired description of your new service. Blank by default.
* <b>duplicate_value</b> - an integer which specifies whether duplicate barcode values will returned as valid or invalid if <b>validation_method</b> is set to <b>database</b> or <b>ondevicedatabase</b> . Input "1" for valid and "0" for invalid. Default value is 1.
* <b>period_start_date</b> - a string which specifies the date when the new service should become active. Can be formatted as MM/DD/YYYY or YYYY-MM-DD ( Examples : 12/20/2012 or 2012-12-20). If this parameter is not specified, the service is always active.
* <b>period_start_time</b> - a string which specifies the time when the new service should become active. Can be formatted as hh:mm:ss or hh:mma ( Examples : 18:30:00 or 6:30pm). If this parameter is not specified, the service is activated at 12:00AM on the specified <b>period_start_date</b> .
* <b>period_end_date</b> - a string which specifies the date when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma ( Examples : 12/20/2012 or 2012-12-20). If this parameter is not specified, the service is always active.
* <b>period_end_time</b> - a string which specifies the time when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma ( Examples : 18:30:00 or 6:30pm). If this parameter is not specified, the service remains active until 11:59:59PM on the specified <b>period_end_date</b> .
* <b>upload_email</b> - a string which specifies the email address the accountholder would like a CSV file of scan data automatically sent to after each upload. If this parameter is not specified, scan data is not emailed.
* <b>upload_email_format</b> - a string which specifies the format of the CSV file to be emailed to the email address specified under <b>upload_email</b> . Possible values are "regular" (do not include scan properties information) and "properties" (includes scan properties). Default value is "regular".
* <b>viewOtherScans</b> - a boolean value which specifies which scans an authorized user can view on their device. If set to 0, the user can only view their own scans. If set to 1, the user can view the scans of every user authorized for the service. This value is set to 1 by default.
* <b>enable_direct_scan</b> - an integer which only needs to be specified if <b>validation_method</b> is set to postback. It specifies that the scans will not be routed through the codeREADr servers but instead go directly to your Postback URL server. Input "1" to enable and "0" to disable. Default value is 0.
* <b>symbologies</b> - an array of numbers which specify the barcode symbologies. By selecting only those symbologies which your app users will scan, the scan process will be quicker and more accurate. See the available symbologies here and the corresponding numbers here.
* <b>enableGPS</b> - a boolean value which makes the service submit GPS location with every scan as a scan property. If set to 1, location will be submitted. If set to 0, it will not be submitted. This value is set to 0 by default. ['Background GPS'.]

<h3>Response</h3>

If your service is successfully created after we receive these variables, we will respond with raw XML containing a status of 1 and your new service ID.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1001</id>
</xml>
~~~

<a name="edit"></a><h2>Editing a Service</h2>

Variables omitted when editing a service will not affect their correspondent service settings.

<h3>Required Variables</h3>

* section must be set to services .
* action must be set to update .
* api_key must be set to your unique API key .
* service_id - an integer which specifies the particular service you'd like to update.

<h3>Optional Variables</h3>

* database_id - a string which only needs to be specified if validation_method is set to database or ondevicedatabase . This needs to be set to the ID of the database the scans will be validated against.
* postback_url - a string which only needs to be specified if validation_method is set to postback . This needs to be set to the destination URL where all scans will be forwarded to. (More info.)
* enable_direct_scan - an integer which only needs to be specified if validation_method is set to postback . It specifies whether the scans will not be routed through codeREADr platform but instead go directly to your Postback URL server. Input "1" to enable and "0" to disable. Default value is 0.
* service_name - a string which specifies what you'd like to rename your service.
* description - a string which specifies the new or modified description of your service.
* duplicate_value - an integer which specifies whether duplicate barcode values will returned as valid or invalid if validation_method is set to database or ondevicedatabase . Input "1" for valid and "0" for invalid. Default value is 1.
* period_start_date - a string which specifies the date when the new service should become active. Can be formatted as MM/DD/YYYY or YYYY-MM-DD ( Examples : 12/20/2012 or 2012-12-20). If this parameter is not specified, the service is always active.
* period_start_time - a string which specifies the time when the new service should become active. Can be formatted as hh:mm:ss or hh:mma ( Examples : 18:30:00 or 6:30pm). If this parameter is not specified, the service is activated at 12:00AM on the specified period_start_date .
* period_end_date - a string which specifies the date when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma ( Examples : 12/20/2012 or 2012-12-20). If this parameter is not specified, the service is always active.
* period_end_time - a string which specifies the time when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma ( Examples : 18:30:00 or 6:30pm). If this parameter is not specified, the service remains active until 11:59:59PM on the specified period_end_date .
* upload_email - a string which specifies the email address the accountholder would like a CSV file of scan data automatically sent to after each upload. If this parameter is not specified, scan data is not emailed.
* upload_email_format - a string which specifies the format of the CSV file to be emailed to the email address specified under upload_email . Possible values are "regular" (do not include scan properties information) and "properties" (includes scan properties). Default values is "regular".
* viewOtherScans - a boolean value which specifies which scans an authorized user can view on their device. If set to 0, the user can only view their own scans. If set to 1, the user can view the scans of every user authorized for the service. This value is set to 1 by default.
* symbologies - an array of numbers which specify the barcode symbologies. By selecting only those symbologies that your app users will be scanning, the scan process will be quicker and more accurate. See the available symbologies here.
* enableGPS - a boolean value which makes the service submit GPS location with every scan as a scan property. If set to 1, location will be submitted. If set to 0, it will not be submitted. This value is set to 0 by default. ['Background GPS'.]

<h3>Response</h3>

If your service is successfully edited after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

<a name="delete"></a><h2>Deleting a Service</h2>

<h3>Required Variables</h3>

* section must be set to services .
* action must be set to delete .
* api_key must be set to your unique API key .
* service_id - an integer which specifies the particular service you'd like to delete. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all services.

<h3>Response</h3>

If your service is successfully deleted after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

<a name="authorize"></a><h2>Authorizing / De-Authorizing Users For Services</h2>

<h3>Required Variables</h3>

* section must be set to services .
* action must be set to adduserpermission or revokeuserpermission .
* api_key must be set to your unique API key .
* service_id - a string which specifies the particular services you'd like to authorize / de-authorize a user for. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all services.
* user_id - a string which specifies the user IDs that you wish to authorize / de-authorize for the specified services. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all users.

<h3>Response</h3>

If your users are successfully authorized / de-authorized for the specified services after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

<a name="add"></a><h2>Adding / Removing Questions from a Service</h2>

<h3>Required Variables</h3>

* section must be set to services .
* action must be set to addquestion or removequestion .
* api_key must be set to your unique API key .
* service_id - a string which specifies the particular services you'd like to add / remove questions from. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all services.
* question_id - a string which specifies the question IDs that you wish to add / remove from the specified services. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword all to include all questions.

<h3>Optional Variables</h3>

* condition - an enum type which specifies the condition on which the question will display. There are four possible values.
    * pre_submit will display the question before the scan is submitted to the server.
    * post_submit will display the question after the scan is submitted to the server.
    * valid_scan will display the question after the scan is submitted to the server, but only if the scan is valid.
    * invalid_scan will display the question after the scan is submitted to the server, but only if the scan is invalid.
    * If the parameter is not specified, the default value is pre_submit .

<h3>Response</h3>

If your questions are successfully added / removed from the specified services after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~


[1]:../README.md#finding
