<a name="head"></a><h1>Overview</h1>

Developers! Want to embed codeREADr into your own application? Use our API to integrate our functionality into your software. Make sure to read this document before you get started. 

Note: Use of our API is only available for accounts with a [Paid Plan] [1].

<div>

<a name="toc"></a><h1>Table of Contents</h1>

<ul>
<li>
Overview
<ul>
<li>
<a href="#finding">Finding Your API Key</a>
</li>
<li>
<a href="#submitting">Submitting Variables</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Postback.md#head">Postback + Direct Scan to URL (DSU)</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Postback.md#default-direct">Default Postback URL vs. Direct Scan to URL</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Postback.md#benefits">DSU Benefits</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Postback.md#variables">Variables Posted To Your Server</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Postback.md#response">Your Response</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#head">API: Services</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#retrieve">Retrieving a Service List</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#create">Creating a Service</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#edit">Editing a Service</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#delete">Deleting a Service</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#authorize">Authorizing / De-Authorizing Users For Services</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Services.md#add">Adding / Removing Questions from a Service</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Users.md#head">API: Users</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Users.md#retrieve">Retrieving a List of Users</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Users.md#create">Creating a User</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Users.md#edit">Editing a User</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Users.md#delete">Deleting a User</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Devices.md#head">API: Devices</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Devices.md#retrieve">Retrieving a List of Devices</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Devices.md#edit">Editing a Device</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#head">API: Databases</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#create">Creating a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#retrieve">Retrieving A List of Databases</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#update">Renaming a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#delete">Deleting a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#clear">Clearing a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#showvalues">Retrieving Values of a Database / Search for Values in a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#upload">Uploading a CSV File to a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#addvalue">Adding a Barcode Value to a Database</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#editvalue">Editing Barcode Responses and Results</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Databases.md#deletevalue">Deleting Values From a Database</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Scans.md#head">API: Scans</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Scans.md#retrieve">Retrieving a List of Scans / Searching Scans</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Scans.md#delete">Deleting Scans</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Questions.md#head">API: Questions and Location Tracking</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Questions.md#retrieve">Retrieving a List of Questions</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Questions.md#create">Creating a Question</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Questions.md#delete">Deleting a Question</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Questions.md#add">Adding an Answer Option</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Questions.md#deleteanswer">Deleting an Answer Option</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Uploads.md#head">API: Uploads</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/Uploads.md#retrieve">Retrieving a List of Uploads</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/ScanProperties.md#head">API: Scan Properties</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/ScanProperties.md#create">Creating a Scan Property</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/ScanProperties.md#retrieve">Retrieving a Scan Property Value</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/ScanProperties.md#update">Updating a Scan Property</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/ScanProperties.md#delete">Deleting a Scan Property</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/BarcodeGenerator.md#head">API: Barcode Generator</a>
<ul>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/BarcodeGenerator.md#generate">Generating a Barcode</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/BarcodeGenerator.md#generate-branded">Generating a Branded Barcode (Paid Plans Only)</a>
</li>
</ul>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/ErrorCodes.md">API: Error Codes</a>
</li>
<li>
<a href="/codeREADr/api/blob/master/1.0/contents/AvailableSymbologies.md">API: Available Symbologies</a>
</li>
</ul>

</div>

<a name="finding"></a><h2>Finding Your API Key</h2>

A valid API key is required for any site functions performed through our API. To locate your API key, sign into codeREADr.com or create an account. Once authenticated, click the “Preferences” link in the site header. Your API key is located in the Admin Settings section.

![API Key Location](https://www.codereadr.com/kb/images/apikey_normal.png)

<a href="#head">Back to Top</a>

<a name="submitting"></a><h2>Submitting Variables</h2>

The codeREADr API is located at:

* https://api.codereadr.com/api/

Every function performed through the API requires at least these three variables to be submitted:

| Variable | Description |
| -------- | ----------- |
| section | A string specifying the section of your account you wish to configure. |
| action | A string specifying the action you wish to perform on that area. |
| api_key | A string with your unique API key. |



You can submit variables in one of four different ways:

* <b>GET</b>

The easiest and most direct method. Just attach variables to the URL.

*Example*:

```
https://api.codereadr.com/api/?section=SECTION_VARIABLE&api_key=YOUR_API_KEY&action=ACTION_VARIABLE
```

* <b>POST</b>

Create an HTML file formatted like the example below, insert your variables and open the file in your browser to send your variables.

*Example*:

~~~ .html
<html>
    <form method="POST" action="https://api.codereadr.com/api/">
        <input type="text" name="api_key" value="YOUR_API_KEY"/>
        <input type="text" name="section" value="SECTION_VARIABLE"/>
        <input type="text" name="action" value="ACTION_VARIABLE"/>
        <input type="submit"/>
    </form>
</html>
~~~

* <b>XML File</b>

Build an XML file to post to https://api.codereadr.com/api/ . Only one file can be submitted - if you submit several files, only one will be processed and the rest ignored.

*Example*:

~~~ .xml
<xml>
    <section>SECTION_VARIABLE</section>
    <action>ACTION_VARIABLE</action>
    <api_key>YOUR_API_KEY</api_key>
</xml>
~~~

* <b>XML String</b>

You can also build an XML string, assign it to the variable named xml and either send it via GET or POST.

*Example*:

~~~ .xml
<xml>
    <section>SECTION_VARIABLE</section>
    <action>ACTION_VARIABLE</action>
    <api_key>YOUR_API_KEY</api_key>
</xml>
~~~

After the API receives the request, it responds with raw XML containing either a success status and requested information, or a failure status and an error description.

<a href="#head">Back to Top</a>

[1]: https://www.codereadr.com/kb/content/14/90/en/api-pricing-and-limits.html
