<a name="head"></a><h1>Overview</h1>

Developers! Want to embed codeREADr into your own application? Use our API to integrate our functionality into your software. Make sure to read this document before you get started. 

Note: Use of our API is only available for accounts with a [Paid Plan] [1].


<a name="toc"></a><h1>Table of Contents</h1>

* Overview
    * [Finding Your API Key](#finding)
    * [Submitting Variables](#submitting)
* [Postback + Direct Scan to URL (DSU)](contents/Postback.md#head)
    * [Default Postback URL vs. Direct Scan to URL](contents/Postback.md#default-direct)
    * [DSU Benefits](contents/Postback.md#benefits)
    * [Variables Posted To Your Server](contents/Postback.md#variables)
    * [Your Response](contents/Postback.md#response)
* [API: Services](contents/Services.md#head)
    * [Retrieving a Service List](contents/Services.md#retrieve)
    * [Creating a Service](contents/Services.md#create)
    * [Editing a Service](contents/Services.md#edit)
    * [Deleting a Service](contents/Services.md#delete)
    * [Authorizing / De-Authorizing Users For Services](contents/Services.md#authorize)
    * [Adding / Removing Questions from a Service](contents/Services.md#add)
* [API: Users](contents/Users.md#head)
    * [Retrieving a List of Users](contents/Users.md#retrieve)
    * [Creating a User](contents/Users.md#create)
    * [Editing a User](contents/Users.md#edit)
    * [Deleting a User](contents/Users.md#delete)
* [API: Devices](contents/Devices.md#head)
    * [Retrieving a List of Devices](contents/Devices.md#retrieve)
    * [Editing a Device](contents/Devices.md#edit)
* [API: Questions and Location Tracking](contents/Questions.md#head)
    * [Retrieving a List of Questions](contents/Questions.md#retrieve)
    * [Creating a Question](contents/Questions.md#create)
    * [Deleting a Question](contents/Questions.md#delete)
    * [Adding an Answer Option](contents/Questions.md#add)
    * [Deleting an Answer Option](contents/Questions.md#deleteanswer)
* [API: Scans](contents/Scans.md#head)
    * [Retrieving a List of Scans / Searching Scans](contents/Scans.md#retrieve)
    * [Deleting Scans](contents/Scans.md#delete)
* [API: Uploads](contents/Uploads.md#head)
    * [Retrieving a List of Uploads](contents/Uploads.md#retrieve)
* [API: Scan Properties](contents/ScanProperties.md#head)
    * [Creating a Scan Property](contents/ScanProperties.md#create)
    * [Retrieving a Scan Property Value](contents/ScanProperties.md#retrieve)
    * [Updating a Scan Property](contents/ScanProperties.md#update)
    * [Deleting a Scan Property](contents/ScanProperties.md#delete)
* [API: Error Codes](contents/ErrorCodes.md)

<a name="finding"></a><h2>Finding Your API Key</h2>

A valid API key is required for any site functions performed through our API. To locate your API key, sign into codeREADr.com or create an account. Once authenticated, click the “Preferences” link in the site header. Your API key is located in the Admin Settings section.

![API Key Location](https://www.codereadr.com/kb/images/apikey_normal.png)

<a href="#head">Back to Top</a>

<a name="submitting"></a><h2>Submitting Variables</h2>

The codeREADr API is located at:

* https://api.codereadr.com/api/

Every function performed through the API requires at least these three variables to be submitted:

* section - a string specifying the section of your account you wish to configure
* action - a string specifying the action you wish to perform on that area
* api_key - a string with your unique API key



You can submit variables in one of four different ways.

* GET

The easiest and most direct method. Just attach variables to the URL.

Example:

```
https://api.codereadr.com/api/?section=SECTION_VARIABLE&api_key=YOUR_API_KEY&action=ACTION_VARIABLE
```

* POST

Create an HTML file formatted like the example below, insert your variables and open the file in your browser to send your variables.

Example:

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

* XML File

Build an XML file to post to https://api.codereadr.com/api/ . Only one file can be submitted - if you submit several files, only one will be processed and the rest ignored.

Example:

```xml
<xml>
    <section>SECTION_VARIABLE</section>
    <action>ACTION_VARIABLE</action>
    <api_key>YOUR_API_KEY</api_key>
</xml>
```

* XML String

You can also build an XML string, assign it to the variable named xml and either send it via GET or POST.

Example:

```xml
<xml>
    <section>SECTION_VARIABLE</section>
    <action>ACTION_VARIABLE</action>
    <api_key>YOUR_API_KEY</api_key>
</xml>
```

After the API receives the request, it responds with raw XML containing either a success status and requested information, or a failure status and an error description.

<a href="#head">Back to Top</a>

[1]: https://www.codereadr.com/kb/content/14/90/en/api-pricing-and-limits.html
