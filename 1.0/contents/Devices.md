<a name="head"></a><h1>API: Devices</h1>

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving a List of Devices</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>devices</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| device_id | An integer or set of integers specifying the set of device IDs you would like us to list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all devices. This parameter is set to <code>all</code> by default. |

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and device information.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <device id="73">
        <udid>cb7e743cf62bc79278890a66e4188afc54670753</udid>
        <devicename>John's Device</devicename>
        <created>2009-11-30 11:28:20</created>
    </device>
</xml>
~~~

[Back to Top](#head)

<a name="edit"></a><h2>Editing a Device</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>devices</code>. |
| action | Must be set to <code>update</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| device_id | An integer which specifies the particular device ID you'd like to edit. |
| device_name | A string which specifies what you'd like to rename the device you're editing. |

<h3>Response</h3>

If your device is successfully edited after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)
