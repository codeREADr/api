<a name="head"></a><h1>API: Barcode Generator</h1>

{page_header_info}
{ "title":"Barcode Generator in codeREADr API",
  "meta":"Learn how to generate a regular and branded barcode with the required and optional variables." }
{page_header_info}

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.
*Note:* The API URL for generating barcodes is different from the normal API URL.
```
https://barcode.codereadr.com/api/?section=barcode&action=generate&api_key=YOUR_API_KEY
```
</quote>

<a name="generate"></a><h2>Generating a Barcode</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>barcode</code>. |
| action | Must be set to <code>generate</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| value | A string which specifies your desired barcode value. Must be 100 characters or less. |

<h3>Response</h3>

If your API request is successful we will respond with the raw barcode image <i>(not XML)</i>.

*Success Example*:

![ScreenShot](https://secure.codereadr.com/images/apidocs_standardbarcode.gif)

If the API request fails we will respond with XML.

*Failure Example*:
~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>0</status>
    <error code="120">Invalid section Parameter</error>
</xml>
~~~

[Back to Top](#head)

<a name="generate-branded"></a><h2>Generating a Branded Barcode (Paid Plans Only)</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>barcode</code>. |
| action | Must be set to <code>generate</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| value | A string which specifies your desired barcode value. Must be 100 characters or less. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| size | An integer between 1 and 10 which specifies the dimensions of your barcode in 50px increments. (Examples: <code>1</code> = 50px, <code>2</code> = 100px, <code>10</code> = 500px). |
| valuesize | An integer between 1 and 10 which specifies the size of the barcode ID text. The default value is <code>4</code>. |
| valueposition | Specifies whether to place the barcode ID above or below the barcode itself. You can input either <code>top</code> or <code>bottom</code> . If this parameter is not set, the default value is <code>bottom</code> . |
| hideframe | When set to <code>1</code> it hides the the black frame around the barcode that is present by default. |
| hidevalue | Hides the Barcode ID text if set to non-null value. If left empty or set to <code>0</code>, the barcode ID is visible. |
| text | Specifies the custom text you would like to place below the barcode. |
| textsize | An integer between 1 and 30 which specifies the pixel height of the custom text below your barcode. (Sizes 8-16 recommended). |
| textalignment | The alignment of the custom text below your barcode. Input <code>L</code> for left-aligned text, <code>C</code> for center-aligned and <code>R</code> for right-aligned. Text is left-aligned by default. |
| logo | The image you would like placed near the barcode. You can post it as a file or specify a URL. Supported file types: GIF, JPG and PNG. |
| logoposition | The position of your custom image in relation to the barcode. You can input <code>top</code> , <code>bottom</code> , <code>left</code> , and <code>right</code> . Set to <code>top</code> by default. |
| filetype | The desired file type of your outputted barcode. You can input either <code>JPG</code> , <code>PNG</code> or <code>GIF</code> . Set to <code>GIF</code> by default. |
| errorcorrection | The desired error correction level of your barcode. Barcodes with lower error correction can be scanned more rapidly, while barcodes with higher error correction can be read even if sections of the code are damaged or missing. You can input either <code>L</code> , <code>M</code> , <code>Q</code> or <code>H</code> . The default value is <code>L</code> . [Learn more here](http://en.wikipedia.org/wiki/Qr_code#Error_correction). |
| barcodetype | The desired format of your outputted barcode. You can input either <code>qr</code> or <code>pdf417</code> . Set to <code>qr</code> by default. |

<h3>Response</h3>

If your API request is successful we will respond with the raw barcode image <i>(not XML)</i>.

*Success Example*:

![ScreenShot](https://secure.codereadr.com/images/apidocs_brandedbarcode.jpg)

If the API request fails we will responde with XML.

*Failure Example*:
~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>0</status>
    <error code="120">Invalid section Parameter</error>
</xml>
~~~

[Back to Top](#head)

[1]:../README.md#finding
