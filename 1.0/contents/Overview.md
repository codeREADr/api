
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
