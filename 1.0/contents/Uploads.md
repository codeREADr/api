<a name="head"></a><h1>API: Uploads</h1>

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving a List of Uploads</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>uploads</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| service_id | An integer or series of integers which specifies the particular services you'd like to search for scans within. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. This parameter is set to <code>all</code> by default. |
| device_id | An integer or series of integers which will return only scans conducted by the specified devices. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. This parameter is set to <code>all</code> by default. |
| user_id | An integer or series of integers which will return only scans conducted by the specified users. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all services. This parameter is set to <code>all</code> by default. |
| limit | An integer which limits the maximum number of results displayed within the list. |
| offset | An integer which offsets the results shown. Only valid if <b>limit</b> is provided. (Example: a limit of 20 and an offset of 5 will display a list of 20 scans that begins with the 5th scan). |

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and scan data.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
    <xml>
        <status>1</status>
        <count>3</count>
        <upload id="13193" device_id="123" service_id="456" user_id="7800" status="1" count="5" timestamp="2011-09-06 16:17:29">
        <upload id="13194" device_id="123" service_id="885" user_id="7800" status="1" count="3" timestamp="2011-09-06 16:20:10">
        <upload id="13195" device_id="1260" service_id="4560" user_id="77" status="1" count="400" timestamp="2011-09-06 16:35:09">
</xml>
~~~

[Back to Top](#head)
