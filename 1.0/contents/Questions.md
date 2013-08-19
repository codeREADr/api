<a name="head"></a><h1>API: Questions and Location Tracking</h1>

Make sure to read the [API Overview](../README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving A List of Questions</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Must be set to <code>questions</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key][1]. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| question_id | An integer or series of integers which specifies the question IDs that you wish to include in the list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all questions. This parameter is set to <code>all</code> by default. |

<h3>Response</h3>

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <question id= 1>
        <status>1</status>
        <text>Would you like soda with your movie?</text>
        <answer id="27">Yes</answer>
        <answer id="28">No</answer>
    </question>
</xml>
~~~

[Back to Top](#head)

<a name="create"></a><h2>Creating a Question</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Mst be set to <code>questions</code>. |
| action | Must be set to <code>create</code>. |
| api_key | Must be set to [your unique API key][1]. |
| question_text | A string which specifies the text of your new question. |

<h3>Optional Variables</h3>

| Variable | Description |
| -------- | ----------- |
| question_type | An enum type which specifies the type of question the user will be presented with. You can set the question_type to <code>manual</code>, <code>manualnumeric</code>, <code>option</code>, <code>dropdown</code>, or <code>gps</code>. |
* <code>manual</code> will create a Short Answer question. The user can manually answer with the device's keyboard.
* <code>manualnumeric</code> will create a Short Answer question limited to numeric entry. The user can manually answer using the device's dial pad.
* <code>option</code> will create a Multiple Choice (Single Answer) question. The user will be prompted to choose one of several options.
* <code>dropdown</code> will create a Multiple Choice (Single Answer) question formatted as a dropdown menu, similar to the "select" HTML element. When the user taps the question, they will be presented with the native picker UI of the OS.
* <code>gps</code> will prompt the user to confirm their current location, as determined by the device's onboard GPS.

<h3>Response</h3>

If your question is successfully created, we will respond with raw XML containing a status of <code>1</code> and the numerical ID of your new question.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1002</id>
</xml>
~~~

[Back to Top](#head)

<a name="delete"></a><h2>Deleting a Question</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Mst be set to <code>questions</code>. |
| action | Must be set to <code>delete</code>. |
| api_key | Must be set to [your unique API key][1]. |
| question_id | An integer or series of integers which specifies the question IDs that you wish to include in the list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all questions. |

<h3>Response</h3>

If you have successfully deleted your question, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="add"></a><h2>Adding an Answer Option</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Mst be set to <code>questions</code>. |
| action | Must be set to <code>addanswer</code>. |
| api_key | Must be set to [your unique API key][1]. |
| question_id | An integer which specifies the numeric question ID you want to add an answer to. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all answers. |
| answer_text | A string which specifies the answer text you want to add to the question. |

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing an ID and status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1</id>
</xml>
~~~

[Back to Top](#head)

<a name="deleteanswer"></a><h2>Deleting an Answer Option</h2>

<h3>Required Variables</h3>

| Variable | Description |
| -------- | ----------- |
| section | Mst be set to <code>questions</code>. |
| action | Must be set to <code>deleteanswer</code>. |
| api_key | Must be set to [your unique API key][1]. |
| answer_id | An integer or series of integers specifying the numerical IDs of the answers you want to remove from a question. |

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing an ID and status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

[1]:../README.md#finding
