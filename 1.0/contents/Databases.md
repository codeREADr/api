<a name="head"></a><h1>API: Databases</h1>

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.

<a name="create"></a><h2>Creating a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>create</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_name | A string which specifies the name of your new database. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| case_sensitivity | A boolean value which specifies whether database values are case sensitive. Once the database is created, this setting cannot be changed. Specify <code>1</code> for case-sensitive validation, or <code>0</code> for case-insensitive validation. Set to <code>0</code> (not case-sensitive) by default. |

<h3>Response</h3>

If your database is successfully created, we will respond with raw XML containing a status of <code>1</code> and your new database ID.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1001</id>
</xml>
```

[Back to Top](#head)

<a name="retrieve"></a><h2>Retrieving A List of Databases</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| database_id | An integer or series of integers which specifies the numeric IDs of the databases you want to list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code> ). Set to <code>all</code> by default.|
| info_level | Possible values are ```names``` and ```services```. Target just the info you need for faster response times. <br/> ```names``` - Only includes the name node (excluding associated services and potentially costly item count). <br/> ```services``` - Includes both name and associated service nodes (excluding the slower item count in the default request). |

<h3>Response</h3>

If we successfully receive your variables, we will respond with raw XML containing status and database information.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <database id="120">
        <name>My tickets</name>
        <count>5000</count>
        <service id="123"/>
        <service id="124"/>
    </database>
    <database id="125">
        <name>My inventory</name>
        <count>1574</count>
        <service id="323"/>
        <service id="524"/>
    </database>
</xml>
```

[Back to Top](#head)

<a name="update"></a><h2>Renaming a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>update</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |
| database_name | A string which specifies the new name of your database. |

<h3>Response</h3>

If your database is successfully renamed, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

<a name="delete"></a><h2>Deleting a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>delete</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database you want to delete. |

<h3>Response</h3>

If your database is successfully deleted, we will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

<a name="clear"></a><h2>Clearing a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>clear</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database you want to clear. |

<h3>Response</h3>

If your database is successfully cleared, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

<a name="showvalues"></a><h2>Retrieving Values of a Database / Search for Values in a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>showvalues</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| value | A string to perform an exact match search against the value. (Example: <code>value=abc</code> will limit results to one value). |
| valuelike | A string to perform a partial match search against the value. (Example: <code>value=abc</code> will match abc1 , 123abc , 123abc123 , etc). |
| response | A string to perform an exact match search against the response. (Example: <code>response=abc</code> will limit results to one value). |
| responselike | A string to perform a partial match search against the response. (Example: <code>responselike=abc</code> will match values with responses abc1 , 123abc , 123abc123 , etc). |
| validity | An integer to filter results by validity. Set to <code>1</code> to show only valid values, and set it to <code>0</code> to show only invalid. |
| limit | An integer which limits the maximum number of results displayed within the list. |
| offset | An integer which offsets the results shown. Only valid if limit is provided. (Example: a limit of 20 and an offset of 5 will display a list of 20 values that begins with the 6th value). |

<h3>Response</h3>

We will respond with raw XML containing a status of <code>1</code>, results count and search results.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <count>2</count>
    <value validity="1">
        <id>A1</id>
        <response>A2</response>
    </value>
    <value validity="1">
        <id>B1</id>
        <response>B2</response>
    </value>
</xml>
```

[Back to Top](#head)

<a name="upload"></a><h2>Uploading a CSV File to a Database</h2>

<b>NOTE:</b> This API is a HTTP multipart/form-data POST request to submit normal variables i.e. `section`, `action`, etc and the actual CSV data file under the param `csvfile`. 

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>upload</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database. |
| csvfile | A CSV file as part of a multipart/form-data POST. (Not the url to the file) For formatting guidelines, see [this page](https://www.codereadr.com/knowledgebase/creating-a-database/). |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| trim_value | Set to `1` to trim or `0` to _not trim_ value white space. Defaults to `1`. |
| is_deferred | Set to `1` to asynchronous import your CSV file. This is recommended for uploads of more than 10,000 values. |

<h3>Response</h3>

If your CSV file is successfully imported, we will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

<h3>API Request Examples</h3>

*Curl Command Example*:

```
curl -F section=databases -F action=upload -F database_id=YOUR_DB_ID -F api_key=YOUR_API_KEY -F csvfile=@./YOUR_LOCAL_FILE.csv https://api.codereadr.com/api/
```

*HTML Form Example*:

```html
<html><body>
    <form action="https://api.codereadr.com/api/" enctype="multipart/form-data" method="POST">
      <input name="api_key" placeholder="YOUR_API_KEY" type="text"> <br/>
      <input name="section" type="hidden" value="databases">
      <input name="action" type="hidden" value="upload">
      <input name="database_id" type="text" placeholder="YOUR_DATABASE_ID">  <br/>
      Choose <i>csvfile</i> <input name="csvfile" type="file">  <br/>
      <input type="submit" value="Import CSV File Into My Database">
    </form>
</body></html>
```

[Link to simple HTML form](https://secure.codereadr.com/apidocs/examples/csv2db.html) that imports the entries of a CSV file into a specified CodeREADr database.


[Back to Top](#head)

<a name="upsertmultivalue"></a><h2>Inserting or Updating Multiple Barcodes</h2>

The <code>upsertmultivalue</code> action allows you to specify up to 100 database values to insert/update as without having to upload a CSV file like you do with the <code>upload</code> action. It's also more flexible than the <code>upload</code> action. You can choose to specify some variables *globally* that will apply to all values in the request but also specify some variables locally to specific values in the request. This means in the same request you can insert/update values to multiple databases. Locally specifying value variables follows the array syntax ```values[0][VARIABLE]``` to ```values[99][VARIABLE]```.

- When a value does not specify it's own local `values[i][database_id]` or `values[i][trim_value]`, the setting falls back to the *global* variable (`database_id` or `trim_value`) if it was specified. 
- The value will be ignored if no local or global `database_id` is specified.
- `trim_value` will default to `1` if  no local or global `trim_value` is specified.

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>upsertmultivalue</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| values | An array of up to 100 database values. |
| values[i]\[value] | A string specifying the barcode value that must be 100 characters or less. ```i``` is the index in the values array. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| database_id&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; | An integer which specifies the numeric ID of the database. Will apply to all values that do not have the local variable set via ```values[i][database_id]```. |
| trim_value | Set to `1` to trim or `0` to _not trim_ value white space. Defaults to `1`. This option applies to all values that do not have the local variable set via ```values[i][trim_value]```. |
| values[i]\[database_id] | An integer which specifies the numeric ID of the database. Only applies to ```value[i]``` and not all values in the array. |
| values[i]\[trim_value] | Set to `1` to trim or `0` to _not trim_ value white space. Only applies to ```value[i]``` and not all values in the array. |
| values[i]\[response] | A string which specifies the barcode value's associated response text. |
| values[i]\[validity] | A boolean type which specifies the validity of the barcode. Input <code>0</code> and the new barcode value will be treated as invalid whenever it is scanned. Set to <code>1</code> (valid) by default. |

<h3>Response</h3>

This action allows you to update your database without first checking the state of the value. If your barcode value is successfully inserted or updated to match your request options, will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

<h3>Example Specifying Variables with XML</h3>

```xml
<xml>
   <action>upsertmultivalue</action>
   <api_key>API_KEY</api_key>
   <database_id>DB_ID</database_id>
   <section>databases</section>
   <trim_value>1</trim_value>
   <values>
      <database_id>36156</database_id>
      <message>Thank you!</message>
      <validity>1</validity>
      <value>ABC</value>
   </values>
   <values>
      <database_id>36156</database_id>
      <message>Hello world!</message>
      <trim_value>0</trim_value>
      <validity>1</validity>
      <value>  spaces  </value>
   </values>
</xml>
```

[Back to Top](#head)

<a name="upsertvalue"></a><h2>Inserting or Updating a Barcode</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>upsertvalue</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database. |
| value | A string which specifies the barcode value. Must be 100 characters or less. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| response | A string which specifies the barcode value's associated response text. |
| validity | A boolean type which specifies the validity of the barcode. Input <code>0</code> and the new barcode value will be treated as invalid whenever it is scanned. Set to <code>1</code> (valid) by default. |
| trim_value | Set to `1` to trim or `0` to _not trim_ value white space. Defaults to `1`. |

<h3>Response</h3>

This action allows you to update your database without first checking the state of the value. If your barcode value is successfully inserted or updated to match your request options, will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

<a name="addvalue"></a><h2>Adding a Barcode Value to a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>addvalue</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database. |
| value | A string which specifies the barcode value. Must be 100 characters or less. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| response | A string which specifies the barcode value's associated response text. |
| validity | A boolean type which specifies the validity of the barcode. Input <code>0</code> and the new barcode value will be treated as invalid whenever it is scanned. Set to <code>1</code> (valid) by default. |
| trim_value | Set to `1` to trim or `0` to _not trim_ value white space. Defaults to `1`. |

<h3>Response</h3>

If your barcode value is successfully added, we will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

<a name="editvalue"></a><h2>Editing Barcode Responses and Results</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>editvalue</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database. |
| value | A string which specifies the barcode value. Must be 100 characters or less. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| response | A string which specifies the barcode value's associated response text. |
| validity | A boolean type which specifies the validity of the barcode. Input <code>0</code> and the new barcode value will be treated as invalid whenever it is scanned. Validity remains unchanged by default. |

<h3>Response</h3>

If your barcode response text and/or validity is successfully edited, we will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

<a name="deletevalue"></a><h2>Deleting Values From a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>deletevalue</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| database_id | An integer which specifies the numeric ID of the database. |
| value | A string which specifies the barcode value. Must be 100 characters or less. |

<h3>Response</h3>

If your barcode value is successfully deleted, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```

[Back to Top](#head)

[1]:../README.md#finding
