<a name="head"></a><h1>API: Services</h1>

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving A Service List</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>services</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| service_id | An integer or set of integers specifying the set of service IDs you would like us to list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. This parameter is set to <code>all</code> by default. |

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

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>services</code>. |
| action | Must be set to <code>create</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| validation_method | An enum type that specifies the service type you desire for your new service. You must set it to one of these options: <code>record</code>, <code>ondevicerecord</code>, <code>database</code>, <code>ondevicedatabase</code>, <code>webview</code>, or <code>postback</code>. |
* <code>record</code> (Record Scans Online)
* <code>ondevicerecord</code> (Record Scans On-Device)
* <code>database</code> (Validate Scans Online)
* <code>ondevicedatabase</code> (Validate Scans On-Device)
* <code>postback</code> ([Postback URL](Postback.md#head))
* <code>webview</code> (View Web Content (no scanning))

If <b>validation_method</b> is set to <code>database</code> or <code>ondevicedatabase</code>:

| Variable | Description |
| -------- | ----------- |
| database_id | A string which must be included and set to the ID of the database the scans will be validated against. |

If <b>validation_method</b> is set to <code>postback</code>:

| Variable | Description |
| -------- | ----------- |
| postback_url | A string which must be included and set to the destination URL where all scans will be forwarded to. ([More info.](Postback.md#head)) |

If <b>validation_method</b> is set to <code>webview</code>:

| Variable | Description |
| -------- | ----------- |
| description | A string which specifies the web content to display. Set to a URL like this ```<curl>https://www.example.com/page.html</curl>``` or HTML code directly i.e. ```<html>...</html>```.<br>Note: including attributes in the opening html tag (i.e. ```<html lang="en">```) is currently not allowed. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| service_name | A string which specifies the desired name of your new service. The default is <code>Service $i</code>, where <code>$i</code> is the next available sequential number. |
| description | A string which specifies the desired description of your new service. Blank by default. |
| duplicate_value | An integer value that specifies the status of a duplicate scan if <code>validation_method</code> is set to ```database``` or ```ondevicedatabase```. Set to ```1``` for _valid_ scan status and ```0``` for _invalid_ scan status. The default status of duplicates are valid (e.g. value set to ```1```). |
| device_duplicate_value | An integer value that specifies the status of a duplicate scan when scanning on-device. It’s only for checking against scans currently stored on the device. Set to ```1``` to make the status of duplicate scans currently on the device _valid_ and set to ```0``` to make them _invalid_. The default status of duplicates on-device are valid (e.g. value set to ```1```). This only applies when the <code>validation_method</code> is set to ```record```, ```ondevicerecord```, ```database``` or ```ondevicedatabase```. NOTE: if the ```duplicate_value``` option is set to ```0``` (invalid) then this option is overridden. |
| period_start_date | A string which specifies the date when the new service should become active. Can be formatted as MM/DD/YYYY or YYYY-MM-DD (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active. |
| period_start_time | A string which specifies the time when the new service should become active. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>18:30:00</code> or <code>6:30pm</code>). If this parameter is not specified, the service is activated at 12:00AM on the specified <b>period_start_date</b>. |
| period_end_date | A string which specifies the date when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active. |
| period_end_time | A string which specifies the time when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: 18:30:00 or 6:30pm). If this parameter is not specified, the service remains active until 11:59:59PM on the specified <b>period_end_date</b>. |
| upload_email | A string which specifies the email address the accountholder would like a CSV file of scan data automatically sent to after each upload. If this parameter is not specified, scan data is not emailed. |
| upload_email_format | A string which specifies the format of the CSV file to be emailed to the email address specified under <b>upload_email</b>. Possible values are <code>regular</code> (do not include scan properties information) and <code>properties</code> (includes scan properties). Default value is <code>regular</code>. |
| viewOtherScans | A boolean value which specifies which scans an authorized user can view on their device. If set to <code>0</code>, the user can only view their own scans. If set to <code>1</code>, the user can view the scans of every user authorized for the service. This value is set to <code>1</code> by default. |
| direct_history_url | Set to the URL you want to loaded in web view when the user clicks the `History` option in the app. Set to empty to disable. |
| direct_lookup_url | Set to the URL you want to loaded in web view when the user clicks the `Lookup` option in the app. Set to empty to disable. |
| enable_direct_scan |  An integer which only needs to be specified if the <b>validation_method</b> is set to `postback`. It specifies that the scans will not be routed through the codeREADr servers but instead go directly to your Postback URL server. Input 1 to enable and 0 to disable. Default value is 0. |
| postback_receiver_only |  Set to `1` if your `postback_url` can only receive. Set to `0` if it can receive and respond with the expected XML. The default value is `0`. |
| postback_real_time_scans |  Set to `1` enable or `0` to disable the postback of each online scan made directly to the server. This variable must be submitted together with the `postback_url` variable to add postback functionality to non-postback service types such as `record`, `database`, etc. It does not work with services of type `postback`. |
| postback_uploaded_scans |  Set to `1` enable or `0` to disable the postback each on-device scan uploaded to the server. This variable must be submitted together with the `postback_url` variable to add postback functionality to non-postback service types such as `record`, `database`, etc. It does not work with services of type `postback`. |
| regex_response_pattern | The first half of a regular expression match and replace pair. Set to a regular expression pattern you want to match in the scan response and replace with `regex_response_replacement`. Set to empty to disable. This variable must be submitted together with `regex_response_replacement`. |
| regex_response_replacement | The second half of a regular expression match and replace pair. Set to the value that will replace the corresponding `regex_response_pattern` match. Set to empty to disable. This variable must be submitted together with `regex_response_pattern`. |
| regex_scan_pattern | The first half of a regular expression match and replace pair. Set to a regular expression pattern you want to match in the scan value and replace with `regex_scan_replacement`. Set to empty to disable. This variable must be submitted together with `regex_scan_replacement`.|
| regex_scan_replacement | The second half of a regular expression match and replace pair. Set to the value that will replace the corresponding `regex_scan_pattern` match. Set to empty to disable. This variable must be submitted together with `regex_scan_pattern`. |
| symbologies | An integer or set of integers specifying the barcode symbolgy IDs. You can specify a single integer or a comma-separated list of integers (Examples: 33 or 33, 34, 12). By selecting only those symbologies which your app users will scan, the scan process will be quicker and more accurate. See the [table of symbology ID numbers](AvailableSymbologies.md). Note: All symbologies are not available to all accounts. Updating the service without submitting the 'symbologies' parameter will reset to default.  |
| auto_next_scan | An integer value to enable or disable the Auto-Next Scan feature. This option is not enabled by default. <br/>Set to `0` to **disable** this feature. <br/>Set to `1` for **Only when valid** mode. <br/>Set to `2` for **Always and save if Error** mode. <br/>Set to `3` for **Always and discard if Error** mode. |
| enableGPS | A boolean value which makes the service submit GPS location with every scan as a scan property. If set to <code>1</code>, location will be submitted. If set to <code>0</code>, it will not be submitted. This value is set to <code>0</code> by default. [Background GPS](https://www.codereadr.com/knowledgebase/gps-location-tracking/). |
| block_camera_scan | A boolean value which specifies if users are allowed to scan barcode using the device's camera. If set to <code>0</code>, users are allowed to scan using device camera. If set to <code>1</code>, users will not be able to scan via the device's camera. This value is set to 0 by default. |
| block_manual_scan | A boolean value which specifies if users are allowed to enter scan values manually. If set to <code>0</code>, users are allowed to enter scan data manually. If set to <code>1</code>, users are not allowed to enter scan data manually. This value is set to 0 by default. |
| block_db_search | A boolean value which specifies if users are allowed to lookup values in database. If set to <code>0</code>, users are allowed to lookup. If set to <code>1</code>, users are not allowed lookup in database. This value is set to 0 by default. |
| auto_sync | Set to `1` to enable <i>Auto Sync</i>. By default we will sync scans saved on-device to codeREADr servers and sync down database updates if the service is an <i>ondevicedatabase</i> type service. Note: currently only on-device databases containing up to <i>50,000 values</i> are supported. Contact us if your database exceeds that limit and learn your options. |
| auto_sync_up_url | Set it to your own <a href="https://www.codereadr.com/apidocs/Postback.md#head">Postback URL</a> to skip us and auto sync scans directly to your server. Only for services with <code>auto_sync</code> enabled. |
| auto_sync_up_delay | An integer value specifying the delay in seconds between attempts to upload scans to the server. Default delay is 2 seconds. Only for services with <code>auto_sync</code> enabled. |
| auto_sync_down_url | Set to `0` to disable automatic downloading of database updates. Users will have to manual download database updates. If you need to re-enable set to `1`. Only for on-device database services with <code>auto_sync</code> enabled. Note: specifying your own cutom URL is not publicly supported at this time. |
| auto_sync_down_delay | An integer value specifying the delay in seconds between checks to sync down new database updates from the server. Default delay is 120 seconds. Only for services with <code>auto_sync</code> enabled. |

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

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>services</code>. |
| action | Must be set to <code>update</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| service_id | An integer which specifies the particular service you'd like to update. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| database_id | A string which only needs to be specified if <b>validation_method</b> is set to <code>database</code> or <code>ondevicedatabase</code>. This needs to be set to the ID of the database the scans will be validated against. |
| direct_history_url | Set to the URL you want to loaded in web view when the user clicks the `History` option in the app. Set to empty to disable. |
| direct_lookup_url | Set to the URL you want to loaded in web view when the user clicks the `Lookup` option in the app. Set to empty to disable. |
| postback_url | A string which only needs to be specified if <b>validation_method</b> is set to <code>postback</code>. This needs to be set to the destination URL wall scans will be forwarded to. [More info](https://www.codereadr.com/knowledgebase/postback-direct-scan-url-dsu/). |
| postback_receiver_only |  Set to `1` if your `postback_url` can only receive. Set to `0` if it can receive and respond with the expected XML. The default value is `0`. |
| postback_real_time_scans |  Set to `1` enable or `0` to disable the postback of each online scan made directly to the server. This variable must be submitted together with the `postback_url` variable to add postback functionality to non-postback service types such as `record`, `database`, etc. It does not work with services of type `postback`. |
| postback_uploaded_scans |  Set to `1` enable or `0` to disable the postback each on-device scan uploaded to the server. This variable must be submitted together with the `postback_url` variable to add postback functionality to non-postback service types such as `record`, `database`, etc. It does not work with services of type `postback`. |
| regex_response_pattern | The first half of a regular expression match and replace pair. Set to a regular expression pattern you want to match in the scan response and replace with `regex_response_replacement`. Set to empty to disable. This variable must be submitted together with `regex_response_replacement`. |
| regex_response_replacement | The second half of a regular expression match and replace pair. Set to the value that will replace the corresponding `regex_response_pattern` match. Set to empty to disable. This variable must be submitted together with `regex_response_pattern`. |
| regex_scan_pattern | The first half of a regular expression match and replace pair. Set to a regular expression pattern you want to match in the scan value and replace with `regex_scan_replacement`. Set to empty to disable. This variable must be submitted together with `regex_scan_replacement`.|
| regex_scan_replacement | The second half of a regular expression match and replace pair. Set to the value that will replace the corresponding `regex_scan_pattern` match. Set to empty to disable. This variable must be submitted together with `regex_scan_pattern`. |
| service_name | A string which specifies what you'd like to rename your service. |
| description | A string which specifies the new or modified description of your service. |
| duplicate_value | An integer value that specifies the status of a duplicate scan if <code>validation_method</code> is set to ```database``` or ```ondevicedatabase```. Set to ```1``` for _valid_ scan status and ```0``` for _invalid_ scan status. The default status of duplicates are valid (e.g. value set to ```1```). |
| device_duplicate_value | An integer value that specifies the status of a duplicate scan when scanning on-device. It’s only for checking against scans currently stored on the device. Set to ```1``` to make the status of duplicate scans currently on the device _valid_ and set to ```0``` to make them _invalid_. The default status of duplicates on-device are valid (e.g. value set to ```1```). This only applies when the <code>validation_method</code> is set to ```record```, ```ondevicerecord```, ```database``` or ```ondevicedatabase```. NOTE: if the ```duplicate_value``` option is set to ```0``` (invalid) then this option is overridden. |
| period_start_date | A string which specifies the date when the new service should become active. Can be formatted as MM/DD/YYYY or YYYY-MM-DD (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active. |
| period_start_time | A string which specifies the time when the new service should become active. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>18:30:00</code> or <code>6:30pm</code>). If this parameter is not specified, the service is activated at 12:00AM on the specified <b>period_start_date</b>. |
| period_end_date | A string which specifies the date when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>12/20/2012</code> or <code>2012-12-20</code>). If this parameter is not specified, the service is always active. |
| period_end_time | A string which specifies the time when the new service should become inactive. Can be formatted as hh:mm:ss or hh:mma (Examples: <code>18:30:00</code> or <code>6:30pm</code>). If this parameter is not specified, the service remains active until 11:59:59PM on the specified <b>period_end_date</b>. |
| upload_email | A string which specifies the email address the accountholder would like a CSV file of scan data automatically sent to after each upload. If this parameter is not specified, scan data is not emailed. |
| upload_email_format | A string which specifies the format of the CSV file to be emailed to the email address specified under <b>upload_email</b>. Possible values are <code>regular</code> (do not include scan properties information) and <code>properties</code> (includes scan properties). Default values is <code>regular</code>. |
| viewOtherScans | A boolean value which specifies which scans an authorized user can view on their device. If set to <code>0</code>, the user can only view their own scans. If set to <code>1</code>, the user can view the scans of every user authorized for the service. This value is set to <code>1</code> by default. |
| symbologies | An integer or set of integers specifying the barcode symbolgy IDs. You can specify a single integer or a comma-separated list of integers (Examples: 33 or 33, 34, 12). By selecting only those symbologies which your app users will scan, the scan process will be quicker and more accurate. See the [table of symbology ID numbers](AvailableSymbologies.md). Note: All symbologies are not available to all accounts. Updating the service without submitting the 'symbologies' parameter will reset to default. |
| auto_next_scan | An integer value to enable or disable the Auto-Next Scan feature. This option is not enabled by default. <br/>Set to `0` to **disable** this feature. <br/>Set to `1` for **Only when valid** mode. <br/>Set to `2` for **Always and save if Error** mode. <br/>Set to `3` for **Always and discard if Error** mode. |
| enableGPS | A boolean value which makes the service submit GPS location with every scan as a scan property. If set to 1, location will be submitted. If set to 0, it will not be submitted. This value is set to 0 by default. [Background GPS](https://www.codereadr.com/knowledgebase/gps-location-tracking/). |
| block_camera_scan | A boolean value which specifies if users are allowed to scan barcode using the device's camera. If set to <code>0</code>, users are allowed to scan using device camera. If set to <code>1</code>, users will not be able to scan via the device's camera. This value is set to 0 by default. |
| block_manual_scan | A boolean value which specifies if users are allowed to enter scan values manually. If set to <code>0</code>, users are allowed to enter scan data manually. If set to <code>1</code>, users are not allowed to enter scan data manually. This value is set to 0 by default. |
| block_db_search | A boolean value which specifies if users are allowed to lookup values in database. If set to <code>0</code>, users are allowed to lookup. If set to <code>1</code>, users are not allowed lookup in database. This value is set to 0 by default. |
| auto_sync | Set to `1` to enable <i>Auto Sync</i>. By default we will sync scans saved on-device to codeREADr servers and sync down database updates if the service is an <i>ondevicedatabase</i> type service. Note: currently only on-device databases containing up to <i>50,000 values</i> are supported. Contact us if your database exceeds that limit and learn your options. |
| auto_sync_up_url | Set it to your own <a href="https://www.codereadr.com/apidocs/Postback.md#head">Postback URL</a> to skip us and auto sync scans directly to your server. Only for services with <code>auto_sync</code> enabled. |
| auto_sync_up_delay | An integer value specifying the delay in seconds between attempts to upload scans to the server. Default delay is 2 seconds. Only for services with <code>auto_sync</code> enabled. |
| auto_sync_down_url | Set to `0` to disable automatic downloading of database updates. Users will have to manual download database updates. If you need to re-enable set to `1`. Only for on-device database services with <code>auto_sync</code> enabled. Note: specifying your own cutom URL is not publicly supported at this time. |
| auto_sync_down_delay | An integer value specifying the delay in seconds between checks to sync down new database updates from the server. Default delay is 120 seconds. Only for services with <code>auto_sync</code> enabled. |

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

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>services</code>. |
| action | Must be set to <code>delete</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| service_id | An integer which specifies the particular service you'd like to delete. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. |

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

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>services</code>. |
| action | Must be set to <code>adduserpermission</code> or <code>revokeuserpermission</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| service_id | A string which specifies the particular services you'd like to authorize / de-authorize a user for. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. |
| user_id | A string which specifies the user IDs that you wish to authorize / de-authorize for the specified services. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all users. |

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

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>services</code>. |
| action | Must be set to <code>addquestion</code> or <code>removequestion</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| service_id | A string which specifies the particular services you'd like to add / remove questions from. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. |
| question_id | A string which specifies the question IDs that you wish to add / remove from the specified services. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all questions. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| condition | An enum type which specifies the condition on which the question will display. There are four possible values: <code>shared_submit</code>, <code>pre_submit</code>, <code>post_submit</code>, <code>valid_scan</code>, <code>invalid_scan</code>. If the parameter is not specified, the default value is <code>pre_submit</code>.|
| required | A string which specifies the question IDs you wish to make mandatory to answer. You can specify a single integer or comma-separated list of integers. Only used when adding questions to a service. |
* <code>shared_submit</code> will display the question under <b>Session Info</b> on the <b>Scan</b> tab and saved answers will be submitted with each scan made in the session.</code>
* <code>pre_submit</code> will display the question before the scan is submitted to the server.
* <code>post_submit</code> will display the question after the scan is submitted to the server.
* <code>valid_scan</code> will display the question after the scan is submitted to the server, but only if the scan is valid.
* <code>invalid_scan</code> will display the question after the scan is submitted to the server, but only if the scan is invalid.

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
