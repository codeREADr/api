<a name="head"></a><h1>API: Databases</h1>

Make sure to read the [API Overview](../README.md) before this document.

<a name="create"></a><h2>Creating a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>create</code>. |
| api_key | Must be set to [your unique API key][1]. |
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
| api_key | Must be set to [your unique API key][1]. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| database_id | An integer or series of integers which specifies the numeric IDs of the databases you want to list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code> ). Set to <code>all</code> by default.

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
| api_key | Must be set to [your unique API key][1]. |
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
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |

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
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |

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
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |

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

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>upload</code>. |
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |
| csvfile | A CSV file. For formatting guidelines, see [this page](https://codereadr.com/kb/content/5/17/en/creating-a-csv-file.html). |

<h3>Response</h3>

If your CSV file is successfully imported, we will respond accordingly with raw XML containing a status of <code>1</code>.

*Example*:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
```
Click [here](https://www.codereadr.com/developer/examples/csv2dbform.php) to use a simple HTML form that imports the entries of a CSV file into a specified codeREADr database.

[Back to Top](#head)

<a name="addvalue"></a><h2>Adding a Barcode Value to a Database</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>databases</code>. |
| action | Must be set to <code>addvalue</code>. |
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |
| value | A string which specifies the barcode value. Must be 100 characters or less. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| response | A string which specifies the barcode value's associated response text. |
| validity | A boolean type which specifies the validity of the barcode. Input <code>0</code> and the new barcode value will be treated as invalid whenever it is scanned. Set to <code>1</code> (valid) by default. |

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
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |
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
| api_key | Must be set to [your unique API key][1]. |
| database_id | An integer which specifies the numeric ID of the database you want to rename. |
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
