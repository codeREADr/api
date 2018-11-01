<a name="head"></a><h1>API: Scans</h1>

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving a List of Scans / Searching Scans</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>scans</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |

<h3>Optional Variables</h3>

| Variables | Description |
| --------- | ----------- |
| keyword | A string which specifies a keyword with which to run a search query. Blank by default. |
| service_id | An integer or series of integers which specifies the particular services you'd like to search for scans within. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. This parameter is set to <code>all</code> by default. |
| device_id | An integer or series of integers which will return only scans conducted by the specified devices. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all devices in your search. This parameter is set to <code>all</code> by default. |
| user_id | An integer or series of integers which will return only scans conducted by the specified users. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all users in your search. This parameter is set to <code>all</code> by default. |
| scan_id | You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>) to only retrieve scans with the specified *IDs*. By default all scans are included in your search. |
| status | An enum type which specifies the scan result type you would like to search within. Input <code>1</code> to only display valid scans, <code>0</code> to only display invalid scans and <code>-1</code> to display scans which could not be validated due to lost Internet connectivity. You can also use a comma-separated list to specify multiple scan result types (Examples: <code>1, 0</code>) or the keyword <code>all</code> to include all scan result types in your search. This parameter is set to <code>all</code> by default. |
| start_date | A date (formatted as YYYY-MM-DD). Use this to search for scans conducted after a given date. Blank by default. |
| start_time | A timestamp (24-hour, formatted as HH:mm:ss). Use this to search for scans conducted after a given time. Only valid if <b>start_date</b> is provided. |
| end_date | A date (formatted as YYYY-MM-DD). Use this to search for scans conducted before a given date. Blank by default. |
| end_time | A timestamp (24-hour, formatted as HH:mm:ss). Use this to search for scans conducted before a given time. Only valid if <b>end_date</b> is provided. |
| upload_id | An integer or comma-separated series of integers which can be used to retrieve scans [from a specific upload](Uploads.md). |
| limit | An integer which limits the maximum number of results displayed within the list. Default value is <code>10000</code>. |
| offset | An integer which offsets the results shown. Only valid if <b>limit</b> is provided. (Example: a limit of 20 and an offset of 5 will display a list of 20 scans that begins with the 5th scan). |
| showProperties | A boolean which toggles showing scan properties in the returned XML. Set it to <code>1</code> to show properties. Default value is <code>0</code> (hide properties). |
| includeProperty | A string which takes a comma-separated list of property names. Only scans that contain these properties will be included in the result set of scans. |
| excludeProperty | A string which takes a comma-separated list of property names. Scans that contain any of these properties will be excluded from the result set of scans. |
| with_property | An array to perform an exact match search for a property value that is present in the scan. Array key stands for the property name, while array value stands for the property value. Example: <code>with_property[mode]=auto&with_property[color]=blue</code> |
| without_property | An array to perform an exact match search for a property value that is <i>not</i> present in the scan. Array key stands for the property name, while array value stands for the property value. Example: <code>without_property[mode]=auto&without_property[color]=blue</code> |
| value | A string to perform an exact match search against the scan value (tid). (Example: <code>value=abc</code>). |
| valuelike | A string to perform a partial match search against the scan value (tid). (Example: <code>value=abc</code> will match abc1, 123abc, 123abc123, etc). |
| response | A string to perform an exact match search against the scan response (result). (Example: <code>response=abc</code>). |
| responselike | A string to perform a partial match search against the scan response (result). (Example: <code>responselike=abc</code> will match values with responses abc1, 123abc, 123abc123, etc). |
| timestamp_received | An integer which toggles the display of timestamp_received XML node. If this variable is set to 1 or 2 the timestamp_received node is added to the XML and will contain the timestamp when the scan was actually received by codeREADr (e.g. scan upload timestamp for on-device made scans). Additionally, if <code>timestamp_received=1</code>, then variables <b>start_date</b>, <b>start_time</b>, <b>end_date</b>, <b>end_time</b> will use timestamp_received column to perform filtering, instead of regular timestamp (which is the timestamp when the scan was made on device). |
| timezone | A string which specifies a timezone for the scan timestamps. Examples: <code>timezone=America/New_York</code>, or <code>timezone=Asia/Hong_Kong</code> works for Beijing, <code>timezone=Europe/London</code> works for London etc.) The parameter is set to codeREADr's local time by default (America/New_York, Eastern Time US & Canada). You can dynamically use the timezone configured by the account holder by setting the parameter to the keyword <b>account</b>.  See the list of [list of Available Timezones](AvailableTimezones.md). |
| timezone_offset | *Deprecated - please use <code>timezone</code> variable instead.* &nbsp;&nbsp; A string which specifies a GMT timezone offset for the scan timestamps. You can dynamically use the timezone configured by the account holder by setting the parameter to the keyword <b>account</b>. (Examples: <code>timezone_offset=account</code>, or <code>timezone_offset=+08:00</code> works for Beijing, <code>timezone_offset=00:00</code> works for London, <code>timezone_offset=-03:00</code> works for Brazil, etc.) The parameter is set to codeREADr's local time by default (-05:00 GMT, Eastern Time US & Canada). See a list of timezone offsets [here](AvailableTimezones.md). |
| order_by | An enum type which specifies the order in which you would like your scan list to be sorted. You must set it from the order_by key set below. For ascending order use the key without the \_desc suffix (e.g. <code>device_id</code>) and for descending use the key with the \_desc suffix (e.g. <code>device_id_desc</code>). You can also use a comma-separated list of keys to specify multiple sub-levels of ordering (e.g. <code>device_id,service_id_desc,timestamp</code>). |
| only_recent |A boolean value which specifies if response should contain only recent scan for each barcode. If set to <code>1</code> response will include only the recent scan for each barcode. Set to <code>0</code> to view all scans of each barcode. This value is set to <code>0</code> by default.|

*order_by key set*:
* <code>barcode</code> or <code>barcode_desc</code> (alphabetical by barcode value)
* <code>device_name</code> or <code>device_name_desc</code> (alphabetical by device name)
* <code>device_id</code> or <code>device_id_desc</code> (numerical by device ID)
* <code>response</code> or <code>response_desc</code> (alphabetical by barcode response)
* <code>scan_id</code> or <code>scan_id_desc</code> (numerical by scan ID)
* <code>service_id</code> or <code>service_id_desc</code> (numerical by service ID)
* <code>service_name</code> or <code>service_name_desc</code> (alphabetical by service name)
* <code>status</code> or <code>status_desc</code> (numerical by validation status)
* <code>timestamp</code> or <code>timestamp_desc</code> (chronological order)
* <code>timestamp_received</code> or <code>timestamp_received_desc</code> (chronological order)
* <code>user_id</code> or <code>user_id_desc</code> (numerical by user ID)
* <code>user_name</code> or <code>user_name_desc</code> (alphabetical by username)

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and scan data.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <count>3</count>
    <scan id="13193">
        <device id="573">iPhone 3</device>
        <service id="927">Lead Retrieval</service>
        <user id="3">demo</user>
        <status>1</status>
        <tid>A1B2C3D</tid>
        <result>Item # 123450. New location on Floor 2, station 4.</result>
        <timestamp>2010-08-06 16:42:35</timestamp>
        <answer qid="386" qtext="Primary Interest:">Product A</answer>
        <answer qid="387" qtext="Action Items:">Call</answer>
        <answer qid="390" qtext="Special Notes:">grub</answer>
        <properties>
            <mode>auto</mode>
        </properties>
    </scan>
    <scan id="13194">
        <device id="579">My android device</device>
        <service id="926">Inventory</service>
        <user id="3">demo</user>
        <status>1</status>
        <tid>A1B2C3D</tid>
        <result>Information has been saved.</result>
        <timestamp>2010-08-06 16:46:09</timestamp>
        <answer qid="389" qtext="Enter Quantity:">24</answer>
        <properties>
            <mode>auto</mode>
            <color>blue</color>
        </properties>
    </scan>
    <scan id="13195">
        <device id="571">new phone</device>
        <service id="926">Inventory</service>
        <user id="3">demo</user>
        <status>1</status>
        <tid>A1B2C3D</tid>
        <result>Information has been saved.</result>
        <timestamp>2010-08-06 16:46:24</timestamp>
        <answer qid="389" qtext="Enter Quantity:">99</answer>
    </scan>
</xml>
~~~

[Back to Top](#head)

<a name="delete"></a><h2>Deleting Scans</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>scans</code>. |
| action | Must be set to <code>delete</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| scan_id | One or more integers specifying the scan(s) you would like to delete. When deleting multiple scans, please separate each integer with commas. |

<h2>Response</h2>

After we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)
