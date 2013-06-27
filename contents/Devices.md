<a name="head"></a><h1>API: Devices</h1>

<a name="retrieve"></a><h2>Retrieving a List of Devices</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>devices</b> .
* <b>action</b> must be set to <b>retrieve</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .

<h3>Optional Variables</h3>

* <b>device_id</b> - an integer or set of integers specifying the set of device IDs you would like us to list. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all devices. This parameter is set to <b>all</b> by default..

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and device information.

Example :

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

<a name="edit"></a><h2>Editing a Device</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>devices</b> .
* <b>action</b> must be set to <b>update</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>device_id</b> - an integer which specifies the particular device ID you'd like to edit.
* <b>device_name</b> - a string which specifies what you'd like to rename the device you're editing.

<h3>Response</h3>

If your device is successfully edited after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~
