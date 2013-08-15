<a name="head"></a><h1>API: Barcode Generator</h1>

Make sure to read the [API Overview](../README.md) before this document.

<a name="generate"></a><h2>Generating a Barcode</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>barcode</b>.
* <b>action</b> must be set to <b>generate</b>.
* <b>api_key</b> must be set to [your unique API key][1].
* <b>value</b> - a string which specifies your desired barcode value. Must be 100 characters or less.

<h3>Response</h3>

If we successfully receive your variables, we will respond accordingly with raw XML containing a barcode image.

Example :

![ScreenShot](https://codereadr.com/kb/images/standardbarcode_normal.gif)

[Back to Top](#head)

<a name="generate-branded"></a><h2>Generating a Branded Barcode (Paid Plans Only)</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>barcode</b>.
* <b>action</b> must be set to <b>generate</b>.
* <b>api_key</b> must be set to [your unique API key][1].
* <b>value</b> - a string which specifies your desired barcode value. Must be 100 characters or less.

<h3>Optinal Variables</h3>

| Name | Type | Description |
| ---- | ---- | ----------- |
| size | integer | An integer between 1 and 10 which specifies the dimensions of your barcode in 50px increments. (Examples: <code>1</code> = 50px, <code>2</code> = 100px, <code>10</code> = 500px). |
| valuesize | integer | An integer between 1 and 10 which specifies the size of the barcode ID text. The default value is <code>4</code>. |
| valueposition | enum | Specifies whether to place the barcode ID above or below the barcode itself. You can input either <code>top</code> or <code>bottom</code> . If this parameter is not set, the default value is <code>bottom</code> . |
| hidevalue | bool | Hides the Barcode ID text if set to non-null value. If left empty or set to <code>0</code>, the barcode ID is visible. |
| text | string | Specifies the custom text you would like to place below the barcode. |
| textsize | integer | An integer between 1 and 30 which specifies the pixel height of the custom text below your barcode. (Sizes 8-16 recommended). |
| textalignment | enum | The alignment of the custom text below your barcode. Input <code>L</code> for left-aligned text, <code>C</code> for center-aligned and <code>R</code> for right-aligned. Text is left-aligned by default. |
| logo | file / string | The image you would like placed near the barcode. You can post it as a file or specify a URL. Supported file types: GIF, JPG and PNG. |
| logoposition |enum| The position of your custom image in relation to the barcode. You can input <code>top</code> , <code>bottom</code> , <code>left</code> , and <code>right</code> . Set to <code>top</code> by default. |
| filetype | enum | The desired file type of your outputted barcode. You can input either <code>JPG</code> , <code>PNG</code> or <code>GIF</code> . Set to <code>GIF</code> by default. |
| errorcorrection | enum | The desired error correction level of your barcode. Barcodes with lower error correction can be scanned more rapidly, while barcodes with higher error correction can be read even if sections of the code are damaged or missing. You can input either <code>L</code> , <code>M</code> , <code>Q</code> or <code>H</code> . The default value is <code>L</code> . [Learn more here](http://en.wikipedia.org/wiki/Qr_code#Error_correction). |
| barcodetype | enum | The desired format of your outputted barcode. You can input either <code>qr</code> or <code>pdf417</code> . Set to <code>qr</code> by default. |

<h3>Response</h3>

If we have successfully received your variables, we will respond with raw XML containing your barcode image.

Example :

![ScreenShot](https://codereadr.com/kb/images/brandedcode_normal.jpg)

[Back to Top](#head)

[1]:../README.md#finding
