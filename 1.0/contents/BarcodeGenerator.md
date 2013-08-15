<a name="head"></a><h1>API: Barcode Generator</h1>

<a name="generate"></a><h2>Generating a Barcode</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>barcode</b> .
* <b>action</b> must be set to <b>generate</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>value</b> - a string which specifies your desired barcode value. Must be 100 characters or less.

<h3>Response</h3>

If we successfully receive your variables, we will respond accordingly with raw XML containing a barcode image.

![ScreenShot](https://codereadr.com/kb/images/standardbarcode_normal.gif)

[Back to Top](#head)

<a name="generate"></a><h2>Generating a Branded Barcode (Paid Plans Only)</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>barcode</b> .
* <b>action</b> must be set to <b>generate</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>value</b> - a string which specifies your desired barcode value. Must be 100 characters or less.

<h3>Optinal Variables</h3>

| Name | Type | Description |
| ---- | ---- | ----------- |
| size | integer | An integer between 1 and 10 which specifies the dimensions of your barcode in 50px increments. ( Examples : 1 = 50px, 2 = 100px, 10 = 500px). |
| valuesize | integer | An integer between 1 and 10 which specifies the size of the barcode ID text. The default value is 4. |
| valueposition | enum | Specifies whether to place the barcode ID above or below the barcode itself. You can input either top or bottom . If this parameter is not set, the default value is bottom . |
| hidevalue | bool | Hides the Barcode ID text if set to non-null value. If left empty or set to 0, the barcode ID is visible. |
| text | string | Specifies the custom text you would like to place below the barcode. |
| textsize | integer	An integer between 1 and 30 which specifies the pixel height of the custom text below your barcode. (Sizes 8-16 recommended). |
| textalignment | enum | The alignment of the custom text below your barcode. Input L for left-aligned text, C for center-aligned and R for right-aligned. Text is left-aligned by default. |
| logo | file / string | The image you would like placed near the barcode. You can post it as a file or specify a URL. Supported file types: GIF, JPG and PNG. |
| logoposition |enum| The position of your custom image in relation to the barcode. You can input top , bottom , left and right . Set to top by default. |
| filetype | enum | The desired file type of your outputted barcode. You can input either JPG , PNG or GIF . Set to GIF by default. |
| errorcorrection | enum | The desired error correction level of your barcode. Barcodes with lower error correction can be scanned more rapidly, while barcodes with higher error correction can be read even if sections of the code are damaged or missing. You can input either L , M , Q or H . The default value is L . [Learn more here](http://en.wikipedia.org/wiki/Qr_code#Error_correction). |
| barcodetype | enum | The desired format of your outputted barcode. You can input either qr or pdf417 . Set to qr by default. |

<h3>Response</h3>

If we have successfully received your variables, we will respond with raw XML containing your barcode image.

Example :

![ScreenShot](https://codereadr.com/kb/images/brandedcode_normal.jpg)

[Back to Top](#head)
