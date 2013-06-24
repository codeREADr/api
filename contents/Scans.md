<h1>API: Scans</h1>

<h2>Required Variables</h2>

* <b>section</b> must be set to <b>scans</b> .
* <b>action</b> must be set to <b>retrieve</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .

<h2>Optional Variables</h2>

* <b>keyword</b> - a string which specifies a keyword with which to run a search query. Blank by default.
* <b>service_id</b> - an integer or series of integers which specifies the particular services you'd like to search for scans within. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all services. This parameter is set to <b>all</b> by default.
* <b>device_id</b> - an integer or series of integers which will return only scans conducted by the specifed devices. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all devices in your search. This parameter is set to <b>all</b> by default.
* <b>user_id</b> - an integer or series of integers which will return only scans conducted by the specified users. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all users in your search. This parameter is set to <b>all</b> by default.
* <b>status</b> - an enum type which specifies the scan result type you would like to search within. Input 1 to only display valid scans, 0 to only display invalid scans and -1 to display scans which could not be validated due to lost Internet connectivity. You can also use a comma-separated list to specify multiple scan result types ( Examples : 1, 0 ) or the keyword <b>all</b> to include all scan result types in your search. This parameter is set to <b>all</b> by default.
* <b>start_date</b> - a date (formatted as YYYY-MM-DD). Use this to search for scans conducted after a given date. Blank by default.
* <b>start_time</b> - a timestamp (24-hour, formatted as HH:mm:ss). Use this to search for scans conducted after a given time. Only valid if <b>start_date</b> is provided.
* <b>end_date</b> - a date (formatted as YYYY-MM-DD). Use this to search for scans conducted before a given date. Blank by default.
* <b>end_time</b> - a timestamp (24-hour, formatted as HH:mm:ss). Use this to search for scans conducted before a given time. Only valid if <b>end_date</b> is provided.
* <b>upload_id</b> - an integer or comma-separated series of integers which can be used to retrieve scans [from a specific upload](Uploads.md) .
* <b>order_by</b> - an enum type which specifies the order in which you would like your scan list to be sorted. You must set it to one of these options:
    * <b>service_name</b> (alphabetical by service name)
    * <b>service_id</b> (numerical by service ID)
    * <b>user_name</b> (alphabetical by username)
    * <b>user_id</b> (numerical by user ID)
    * <b>device_name</b> (alphabetical by device name)
    * <b>device_id</b> (numerical by device ID)
    * <b>barcode</b> (alphabetical by barcode value)
    * <b>status</b> (numerical by validation status)
    * <b>response</b> (alphabetical by barcode response)
    * <b>timestamp</b> (chronological order)
* <b>order_desc</b> - a boolean type which specifies the order in which your scan list will be provided. Input any value to display scan data in descending order. If this variable is left blank, scan data will be displayed in ascending order.
* <b>limit</b> - an integer which limits the maximum number of results displayed within the list. Default value is 10000.
* <b>offset</b> - an integer which offsets the results shown. Only valid if <b>limit</b> is provided. ( Example : a limit of 20 and an offset of 5 will display a list of 20 scans that begins with the 5th scan.)
* <b>showProperties</b> - a boolean which toggles showing scan properties in the returned XML. Set it to 1 to show properties. Default value is 0 (hide properties).
* <b>includeProperty</b> - a string which takes a comma-separated list of property names. Only scans that contain these properties will be included in the result set of scans.
* <b>excludeProperty</b> - a string which takes a comma-separated list of property names. Scans that contain any of these properties will be excluded from the result set of scans.
* <b>with_property</b> - an array to perform an exact match search for a property value that is present in the scan. Array key stands for the property name, while array value stands for the property value. Example: with_property[mode]=auto&with_property[color]=blue
* <b>without_property</b> - an array to perform an exact match search for a property value that is <i>not</i> present in the scan. Array key stands for the property name, while array value stands for the property value. Example: without_property[mode]=auto&without_property[color]=blue
* <b>value</b> - a string to perform an exact match search against the scan value (tid). (Example: value=abc )
* <b>valuelike</b> - a string to perform a partial match search against the scan value (tid). (Example: value=abc will match abc1 , 123abc , 123abc123 , etc)
* <b>response</b> - a string to perform an exact match search against the scan response (result). (Example: response=abc )
* <b>responselike</b> - a string to perform a partial match search against the scan response (result). (Example: responselike=abc will match values with responses abc1 , 123abc , 123abc123 , etc)

<h2>Response</h2>

After we receive these variables, we will respond with raw XML containing status and scan data.

Example:

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

<h2>Deleting Scans</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>scans</b>.
* <b>action</b> must be set to <b>delete</b>.
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>scan_id</b> one or more integers specifying the scan(s) you would like to delete. When deleting multiple scans, please separate each integer with commas.

<h2>Response</h2>

After we receive these variables, we will respond with raw XML containing a status of 1.

Example:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~
