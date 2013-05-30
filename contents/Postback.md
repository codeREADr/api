<h1>Postback and Direct Scan to URL (DSU)</h1>

Postback URLs are used to relay data from codeREADr to the URL of your choice. This is one of codeREADr's most valuable features. [We know of IT companies and independent developers who have created new services and even businesses based on this codeREADr feature.] 

<h2>Default Postback URL vs. Direct Scan to URL (DSU)</h2>

When using our default Postback URL service  type, data goes from the scanning device to codeREADr's servers and then gets relayed to your postback URL. This allows us to store the data for use with our managing features such as history review and filtered data exporting. Postback URL also offer the benefit of batch scan upload from the device in cases where internet connectivity is lost. However, we also provide an option to bypass our servers and scan directly to your URL - it's called Direct Scan to URL (DSU). 

<h2>DSU Benefits:</h2>

* The app will POST scan data directly to your URL allowing you to keep your scan data completely contained within your organization.
* You can use LAN (local area network) URLs as long as the device is also on that LAN.
* It is inherently faster because scan data goes directly to you and not through our servers.
* All scan data remains completely private because it never comes to our servers.

Note: If required, with DSU you will have to create your own history URL for in-app scan review and your own database look-up URL.

<h2>Variables Posted To Your Server</h2>

| Name | Description |
| ---- | ----------- |
| tid  | The scanned barcode's value. |
| sid  | The numeric ID of the service the scan was made under. |
| udid | The unique device ID of the scanner. |
| userid | The numeric ID of the user who performed the scan. |
| questions | An array of question texts with numeric question IDs as indices. This variable is only sent if the service contains data collection questions. |
| answers | An array of corresponding answers with numeric question IDs as indices. This variable is only sent if service contains data collection questions. In case of multiple answers given, they are separated by a delimiter, which is |^|, so you can split by it. |

These variables are sent via HTTP POST with every scan. Grabbing these results may vary from language to language, so we suggest looking up how to capture POST variables if you do not know how to do so.

<h2>Your Response</h2>

Default Postback Response: In order for our servers to pass a success or failure message back to the device, you must supply us with an XML response containing three nodes (it was formerly two nodes).

DSU Response: In order to pass a success or failure message back to the device, you must supply an XML response containing three nodes.
