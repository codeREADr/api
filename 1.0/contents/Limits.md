<a name="head"></a><h1>API: Limits</h1>

Make sure to read the [API Overview](../README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving Your API Limits</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>limits</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](../README.md#finding). |

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status 
and your account's API request limits. You will receive your `limit` and how many
requests you have `left` for each time metric currently tracked for your account.
The remaining requests will reset to your `limit` after the given time metric has
past.

Note: Unlimited is represented by `-1` and you may notice it under the `day` metric
for a limited time.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="utf-8"?>
<xml>
    <status>1</status>
    <minute left="18" limit="30"/>
    <day left="9000" limit="21600"/>
</xml>

~~~

[Back to Top](#head)
