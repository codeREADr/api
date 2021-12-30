<a name="head"></a><h1>Postback URL and Postback DSU (Direct Scan to URL)</h1>

Postback is used to direct data from CodeREADr to the URL of your choice. This is one of our most valuable features.

<a name="default-direct"></a><h2>Postback URL vs. Postback DSU (Direct Scan to URL)</h2>

When a CodeREADr service is configured with a <b>Postback URL</b>, by default the data is sent indirectly. The data goes from the scanning device to CodeREADr's servers and then gets relayed from our servers to your Postback URL. This allows us to store the data and provide you with data management features such as history review and filtered data exporting. However, you can also configure your <i>Postback</i> as <b>Direct Scan to URL (DSU)</b> to bypass our servers and scan directly to your URL.

CodeREADr also supports various offline scanning use cases (where scans are first saved on-device and later synced when internet connectivity is available). On-device scans can be synced on-demand by app-users with "batch scan upload" or automatically in the background. Postback DSU only supports auto sync whereas normal Postback URL supports both auto sync and manual batch upload.

The last difference is Postback DSU doess not support postback templates. On codereadr.com you can configure your Postback URL to use a Postback Template to where you define the variables you want your scan data to be posted under.

[Back to Top](#head)

<a name="benefits"></a><h2>Postback DSU Benefits</h2>

* The app will POST scan data directly to your URL allowing you to keep your scan data completely contained within your organization.
* You can use LAN (local area network) URLs as long as the device is also on that LAN.
* It is inherently faster because scan data goes directly to you and not through our servers.
* All scan data remains completely private because it never comes to our servers.

Note: If required, with DSU you will have to create your own history URL for in-app scan review and your own database look-up URL.

[Back to Top](#head)

<a name="variables"></a><h2>Variables Posted To Your Server</h2>

Note: These are default variable names. With our website you have the option to create and configure your postback to use a template defining custom variable names.

| Name | Description |
| ---- | ----------- |
| tid  | The scanned barcode's value. |
| sid  | The numeric ID of the service the scan was made under. |
| udid | The unique device ID of the scanner. |
| userid | The numeric ID of the user who performed the scan. |
| scanid | *(Conditional)* The Scan record ID. This will only be submitted to DSU Postbacks on secondary submits and only if your DSU Postback returned a scan ID on the primary submit. |
| status | *(Conditional)* The existing validation status `(1 , 0, -1)` of the Scan record at the time it is being postback to your URL. |
| text | *(Conditional)* The existing text that was recorded with the Scan record as the response message to the scan submit. |
| scanned_at_utc | UTC timestamp of when the Scan record was made i.e. ```2021-12-31 23:59:59```.  |
| received_at_utc | *(Conditional)*  UTC timestamp of when the Scan record was received by our servers i.e. ```2021-12-31 23:59:59```. This can be different if the Scan was recorded on-device and then uploaded at a later time.  _(Not available to DSU postbacks.)_ |
| questions | An array of question texts with numeric question IDs as indices. This variable is only sent if the service contains data collection questions. Note: Only regular Postback services receive this variable, DSU services only receive the answers variable. |
| answers | An array of corresponding answers with numeric question IDs as indices. This variable is only sent if service contains data collection questions. In case of multiple answers given, they are separated by a delimiter, which is <code>&#124;^&#124;</code>, so you can split by it. |
| *property names* | The scan property variables posted depend on the configuration of your service. A few existing scan property variables are ```capture_type``` (i.e. camera scan, manual entry, value lookup), ```time_zone``` (of the device), ```gps_location``` (background location collection).|

These variables are sent via HTTP POST with every scan. Processing these results may vary with different programming languages, so we suggest looking up how to capture POST variables if you do not know how to do so.

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

*Webify Response – HTML Example*:

If you return <strong>&lt;html&gt;...&lt;/html&gt;</strong> code in the <strong>&lt;text&gt;…&lt;/text&gt;</strong> node then in the app the response area will display as html instead of plain text. Please note that in the example below the HTML is XML escaped because it's not part of the defined XML response format. It's just content being returned in the defined <strong>text</strong> node.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <message>
        <status>1</status>
        <text>
&lt;html&gt;
   &lt;body&gt;
      &lt;h1&gt;Hello World!&lt;/h1&gt;
   &lt;/body&gt;
&lt;/html&gt;
        </text>
    </message>
</xml>
```

*Webify Response – URL Example*:

If you return <strong>&lt;curl&gt;YOUR URL&lt;/curl&gt;</strong> in the <strong>&lt;text&gt;…&lt;/text&gt;</strong> node then in the app the response area will load your URL in a web view instead of display as plain text. Please note that in the example below the &lt;curl&gt;...&lt;/curl&gt; tag is XML escaped because it's just content being returned in the defined <strong>text</strong> node.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <message>
        <status>1</status>
        <text>
&lt;curl&gt;https://www.example.com/hello.html&lt;/curl&gt;
        </text>
    </message>
</xml>
```
Please note that the non-DSU postback response size is limited to 10KB. Any data exceeding that size will be stripped out.

The app waits for your server response for 15 seconds. If the app does not receive one after that time, the request is cancelled and the app displays an error message.

Make sure your response's content-type is set to <code>text-xml</code>, regardless of your communication method. (Example: When using PHP, include the line <code>header('Content-type: text/xml');</code> in your response).

All special XML entities must be encoded. If you see the message below, your response contains illegal XML characters:

```
XML Parsing Error: not well-formed
```

[Back to Top](#head)

<a name="extras"></a><h2>Related Links</h2>
- [CodeREADr server IPs to whitelist](https://secure.codereadr.com/account/integrations/postback) _(requires login)_
- [KB - Postback URL and DSU Variables](https://www.codereadr.com/knowledgebase/postback-url-and-dsu-variables/)
- [KB - Postback URL](https://www.codereadr.com/knowledgebase/postback-url/)
- [KB - Direct Scan to URL (DSU)](https://www.codereadr.com/knowledgebase/direct-scan-url/)

[Back to Top](#head)
