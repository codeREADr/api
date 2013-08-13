<a name="head"></a><h1>API: Scan Properties</h1>

<a name="create"></a><h2>Creating a Scan Property</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>scan_properties</b> .
* <b>action</b> must be set to <b>create</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>scan_id</b> - an integer or set of integers specifying the set of scan IDs you would like to create property for. You can specify a single integer or a comma-separated list of integers (Examples : 1005 or 1005,1010,1254 ).
* <b>name</b> - a string which specifies the name of your new property. Case-sensitive. Limited to 100 characters.
* <b>value</b> - a string which specifies the value of your new property. Case-sensitive. Limited to 100 characters.

<h3>Response</h3>

If your scan property is successfully created, we will respond with raw XML containing a status of 1.

Example:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="retrieve"></a><h2>Retrieving A Scan Property Value</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>scan_properties</b> .
* <b>action</b> must be set to <b>retrieve</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>scan_id</b> - an integer which specifies your scan ID.
* <b>name</b> - a string which specifies the name of the property. Not case sensitive. Limited to 100 characters.

<h3>Response</h3>

If we successfully receive your variables, we will respond with raw XML containing status and scan property information.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <value>40820</value>
</xml>
~~~

[Back to Top](#head)

<a name="update"></a><h2>Updating a Scan Property</h2>
Same as [Creating a Scan Property](#create)

[Back to Top](#head)

<a name="delete"></a><h2>Deleting a Scan Property</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>scan_properties</b> .
* <b>action</b> must be set to <b>delete</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>scan_id</b> - an integer which specifies your scan ID.
* <b>name</b> - a string which specifies the name of the property. Case-sensitive. Limited to 100 characters.

<h3>Response</h3>

If your scan property is successfully deleted, we will respond accordingly with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)
