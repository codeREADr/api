<a name="head"></a><h1>API: Services</h1>

Make sure to read the API Introduction before this document.

<a name="retrieve"></a><h2>Retrieving A Service List</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b>.
* <b>action</b> must be set to <b>retrieve</b>.
* <b>api_key</b> must be set to [your unique API key][1].

<h3>Optional Variables</h3>

* <b>service_id</b> - an integer or set of integers specifying the set of service IDs you would like us to list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. This parameter is set to <code>all</code> by default.

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and service information.

*Example*:

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

[Back to Top](#head)

<a name="create"></a><h2>Creating a Service</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b>.
* <b>action</b> must be set to <b>create</b>.
* <b>api_key</b> must be set to [your unique API key][1].
* <b>validation_method</b> - an enum type that specifies the service type you desire for your new service. You must set it to one of these options:
    * <b>record</b> (Record Scans Online)
    * <b>ondevicerecord</b> (Record Scans On-Device)
    * <b>database</b> (Validate Scans Online)
    * <b>ondevicedatabase</b> (Validate Scans On-Device)
    * <b>postback</b> ([Postback URL](Postback.md#head))

If <b>validation_method</b> is set to <code>database</code> or <code>ondevicedatabase</code>:

* <b>database_id</b> - a string which must be included and set to the ID of the database the scans will be validated against.

If <b>validation_method</b> is set to <code>postback</code>:

* <b>postback_url</b> - a string which must be included and set to the destination URL where all scans will be forwarded to. ([More info.](Postback.md#head))

<h3>Optional Variables</h3>

* <b>service_name</b> - a string which specifies the desired name of your new service. The default is <code>Service $i</code>, where <code>$i</code> is the next available sequential number.
* <b>description</b> - a string which specifies the desired description of your new service. Blank by default.
* <b>duplicate_value</b> - an integer which specifies whether duplicate barcode values will returned as valid or invalid if <b>validation_method</b> is set to <code>database</code> or <code>ondevicedatabase</code> . Input <code>1</code> for valid and <code>0</code> for invalid. Default value is <code>1</code>.
* <b>period_start_date</b> - a string which specifies the date when the new service should become active. Can be formatted as MM/DD/YYYY or YYYY-MM-DD (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active.
* <b>period_start_time</b> - a string which specifies the time when the new service should become active. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>18:30:00</code> or <code>6:30pm</code>). If this parameter is not specified, the service is activated at 12:00AM on the specified <b>period_start_date</b>.
* <b>period_end_date</b> - a string which specifies the date when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active.
* <b>period_end_time</b> - a string which specifies the time when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: 18:30:00 or 6:30pm). If this parameter is not specified, the service remains active until 11:59:59PM on the specified <b>period_end_date</b>.
* <b>upload_email</b> - a string which specifies the email address the accountholder would like a CSV file of scan data automatically sent to after each upload. If this parameter is not specified, scan data is not emailed.
* <b>upload_email_format</b> - a string which specifies the format of the CSV file to be emailed to the email address specified under <b>upload_email</b>. Possible values are <code>regular</code> (do not include scan properties information) and <code>properties</code> (includes scan properties). Default value is <code>regular</code>.
* <b>viewOtherScans</b> - a boolean value which specifies which scans an authorized user can view on their device. If set to <code>0</code>, the user can only view their own scans. If set to <code>1</code>, the user can view the scans of every user authorized for the service. This value is set to <code>1</code> by default.
* <b>enable_direct_scan</b> - an integer which only needs to be specified if <b>validation_method</b> is set to <code>postback</code>. It specifies that the scans will not be routed through the codeREADr servers but instead go directly to your Postback URL server. Input <code>1</code> to enable and <code>0</code> to disable. Default value is <code>0</code>.
* <b>symbologies</b> - an array of numbers which specify the barcode symbologies. By selecting only those symbologies which your app users will scan, the scan process will be quicker and more accurate. See the available symbologies here and the corresponding numbers [here](./AvailableSymobologies.md).
* <b>enableGPS</b> - a boolean value which makes the service submit GPS location with every scan as a scan property. If set to <code>1</code>, location will be submitted. If set to <code>0</code>, it will not be submitted. This value is set to <code>0</code> by default. [Background GPS](https://www.codereadr.com/kb/content/6/30/en/gps-location-tracking.html?highlight=gps).

<h3>Response</h3>

If your service is successfully created after we receive these variables, we will respond with raw XML containing a status of <code>1</code> and your new service ID.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1001</id>
</xml>
~~~

[Back to Top](#head)

<a name="edit"></a><h2>Editing a Service</h2>

Variables omitted when editing a service will not affect their correspondent service settings.

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b>.
* <b>action</b> must be set to <b>update</b>.
* <b>api_key</b> must be set to [your unique API key][1].
* <b>service_id</b> - an integer which specifies the particular service you'd like to update.

<h3>Optional Variables</h3>

* <b>database_id</b> - a string which only needs to be specified if <b>validation_method</b> is set to database or ondevicedatabase . This needs to be set to the ID of the database the scans will be validated against.
* <b>postback_url</b> - a string which only needs to be specified if <b>validation_method</b> is set to postback . This needs to be set to the destination URL where all scans will be forwarded to. [More info](https://codereadr.com/kb/content/14/69/en/postback-direct-scan-to-url-dsu.html).
* <b>enable_direct_scan</b> - an integer which only needs to be specified if <b>validation_method</b> is set to postback . It specifies whether the scans will not be routed through codeREADr platform but instead go directly to your Postback URL server. Input <code>1</code> to enable and <code>0</code> to disable. Default value is <code>0</code>.
* <b>service_name</b> - a string which specifies what you'd like to rename your service.
* <b>description</b> - a string which specifies the new or modified description of your service.
* <b>duplicate_value</b> - an integer which specifies whether duplicate barcode values will returned as valid or invalid if <b>validation_method</b> is set to database or ondevicedatabase . Input <code>1</code> for valid and <code>0</code> for invalid. Default value is <code>1</code>.
* <b>period_start_date</b> - a string which specifies the date when the new service should become active. Can be formatted as MM/DD/YYYY or YYYY-MM-DD (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active.
* <b>period_start_time</b> - a string which specifies the time when the new service should become active. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>18:30:00</code> or <code>6:30pm</code>). If this parameter is not specified, the service is activated at 12:00AM on the specified <b>period_start_date</b>.
* <b>period_end_date</b> - a string which specifies the date when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active.
* <b>period_end_time</b> - a string which specifies the time when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>18:30:00</code> or <code>6:30pm</code>). If this parameter is not specified, the service remains active until 11:59:59PM on the specified <b>period_end_date</b>.
* <b>upload_email</b> - a string which specifies the email address the accountholder would like a CSV file of scan data automatically sent to after each upload. If this parameter is not specified, scan data is not emailed.
* <b>upload_email_format</b> - a string which specifies the format of the CSV file to be emailed to the email address specified under <b>upload_email</b>. Possible values are <code>regular</code> (do not include scan properties information) and <code>properties</code> (includes scan properties). Default values is <code>regular</code>.
* <b>viewOtherScans</b> - a boolean value which specifies which scans an authorized user can view on their device. If set to <code>0</code>, the user can only view their own scans. If set to <code>1</code>, the user can view the scans of every user authorized for the service. This value is set to <code>1</code> by default.
* <b>symbologies</b> - an array of numbers which specify the barcode symbologies. By selecting only those symbologies that your app users will be scanning, the scan process will be quicker and more accurate. See the available symbologies [here](./AvailableSymobologies.md).
* <b>enableGPS</b> - a boolean value which makes the service submit GPS location with every scan as a scan property. If set to 1, location will be submitted. If set to 0, it will not be submitted. This value is set to 0 by default. [Background GPS](https://www.codereadr.com/kb/content/6/30/en/gps-location-tracking.html?highlight=gps).

<h3>Response</h3>

If your service is successfully edited after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="delete"></a><h2>Deleting a Service</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b>.
* <b>action</b> must be set to <b>delete</b>.
* <b>api_key</b> must be set to [your unique API key](..README.md#finding).
* <b>service_id</b> - an integer which specifies the particular service you'd like to delete. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services.

<h3>Response</h3>

If your service is successfully deleted after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="authorize"></a><h2>Authorizing / De-Authorizing Users For Services</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b>.
* <b>action</b> must be set to <b>adduserpermission</b> or <b>revokeuserpermission</b>.
* <b>api_key</b> must be set to [your unique API key](../README.md#finding).
* <b>service_id</b> - a string which specifies the particular services you'd like to authorize / de-authorize a user for. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services.
* <b>user_id</b> - a string which specifies the user IDs that you wish to authorize / de-authorize for the specified services. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all users.

<h3>Response</h3>

If your users are successfully authorized / de-authorized for the specified services after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="add"></a><h2>Adding / Removing Questions from a Service</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>services</b>.
* <b>action</b> must be set to <b>addquestion</b> or <b>removequestion</b>.
* <b>api_key</b> must be set to [your unique API key](../README.md#finding).
* <b>service_id</b> - a string which specifies the particular services you'd like to add / remove questions from. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services.
* <b>question_id</b> - a string which specifies the question IDs that you wish to add / remove from the specified services. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all questions.

<h3>Optional Variables</h3>

* <b>condition</b> - an enum type which specifies the condition on which the question will display. There are four possible values.
    * <b>pre_submit</b> will display the question before the scan is submitted to the server.
    * <b>post_submit</b> will display the question after the scan is submitted to the server.
    * <b>valid_scan</b> will display the question after the scan is submitted to the server, but only if the scan is valid.
    * <b>invalid_scan</b> will display the question after the scan is submitted to the server, but only if the scan is invalid.

If the parameter is not specified, the default value is <b>pre_submit</b> .

<h3>Response</h3>

If your questions are successfully added / removed from the specified services after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

[1]:../README.md#finding
