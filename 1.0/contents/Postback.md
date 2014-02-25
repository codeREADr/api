<a name="head"></a><h1>Postback and Direct Scan to URL (DSU)</h1>

Postback URLs are used to relay data from codeREADr to the URL of your choice. This is one of codeREADr's most valuable features. [We know of IT companies and independent developers who have created new services and even businesses based on this codeREADr feature.] 

<a name="default-direct"></a><h2>Default Postback URL vs. Direct Scan to URL (DSU)</h2>

When using our default Postback URL service  type, data goes from the scanning device to codeREADr's servers and then gets relayed to your postback URL. This allows us to store the data for use with our managing features such as history review and filtered data exporting. Postback URL also offer the benefit of batch scan upload from the device in cases where internet connectivity is lost. However, we also provide an option to bypass our servers and scan directly to your URL - it's called Direct Scan to URL (DSU). 

[Back to Top](#head)

<a name="benefits"></a><h2>DSU Benefits</h2>

* The app will POST scan data directly to your URL allowing you to keep your scan data completely contained within your organization.
* You can use LAN (local area network) URLs as long as the device is also on that LAN.
* It is inherently faster because scan data goes directly to you and not through our servers.
* All scan data remains completely private because it never comes to our servers.

Note: If required, with DSU you will have to create your own history URL for in-app scan review and your own database look-up URL.

[Back to Top](#head)

<a name="variables"></a><h2>Variables Posted To Your Server</h2>

| Name | Description |
| ---- | ----------- |
| tid  | The scanned barcode's value. |
| sid  | The numeric ID of the service the scan was made under. |
| udid | The unique device ID of the scanner. |
| userid | The numeric ID of the user who performed the scan. |
| questions | An array of question texts with numeric question IDs as indices. This variable is only sent if the service contains data collection questions. *Note: Only regular Postback services receive this variable, DSU services only receive the answers variable.* |
| answers | An array of corresponding answers with numeric question IDs as indices. This variable is only sent if service contains data collection questions. In case of multiple answers given, they are separated by a delimiter, which is <code>&#124;^&#124;</code>, so you can split by it. |
| properties_name | Existing scan properties may include Capture Type, Mask Matched (for pattern validation services), Time Zone and GPS Location, depending on the configuration of your service.|

These variables are sent via HTTP POST with every scan. Grabbing these results may vary from language to language, so we suggest looking up how to capture POST variables if you do not know how to do so.

[Back to Top](#head)

<a name="response"></a><h2>Your Response</h2>

Default Postback Response: In order for our servers to pass a success or failure message back to the device, you must supply us with an XML response containing three nodes (it was formerly two nodes).

DSU Response: In order to pass a success or failure message back to the device, you must supply an XML response containing three nodes.

* <b>message</b> - Parent node for scans response nodes.
* <b>status</b> -  This must be set to either <code>1</code> (Success) or <code>0</code> (Failure).
* <b>text</b> -  The text the user will see on their device under the success status.

*General Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <message>
        <status>1</status>
        <text>Thank you for scanning with codeREADr</text>
    </message>
</xml>
```

*PHP Example*:

```php
header("Content-type: text/xml");
echo '<?xml version="1.0" encoding="UTF-8"?>';
echo '<xml>';
echo '    <message>';
echo '        <status>1</status>';
echo '        <text>Thank you for scanning with codeREADr</text>';
echo '    </message>';
echo '</xml>';
```

Please note that the non-DSU postback response size is limited to 10KB. Any data exceeding that size will be stripped out.

The app waits for your server response for 15 seconds. If the app does not receive one after that time, the request is cancelled and the app displays an error message.

Make sure your response's content-type is set to <code>text-xml</code>, regardless of your communication method. (Example: When using PHP, include the line <code>header('Content-type: text/xml');</code> in your response).

All special XML entities must be encoded. If you see the message below, your response contains illegal XML characters:

```
XML Parsing Error: not well-formed
```

[Back to Top](#head)
