<a name="head"></a><h1>API: Questions and Location Tracking</h1>

<a name="retrieve"></a><h2>Retrieving A List of Questions</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>questions</b> .
* <b>action</b> must be set to <b>retrieve</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md/#finding) .

<h3>Optional Variables</h3>

* <b>question_id</b> - an integer or series of integers which specifies the question IDs that you wish to include in the list. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all questions. This parameter is set to <b>all</b> by default.

<h3>Response</h3>

Example :

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

* <b>section</b> must be set to <b>questions</b> .
* <b>action</b> must be set to <b>create</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>question_text</b> - a string which specifies the text of your new question.

<h3>Optional Variables</h3>

* <b>question_type</b> - an enum type which specifies the type of question the user will be presented with.
    * <b>manual</b> will create a Short Answer question. The user can manually answer with the device's keyboard.
    * <b>manualnumeric</b> will create a Short Answer question limited to numeric entry. The user can manually answer using the device's dial pad.
    * <b>option</b> will create a Multiple Choice (Single Answer) question. The user will be prompted to choose one of several options.
        or
    * <b>dropdown</b> will create a Multiple Choice (Single Answer) question formatted as a dropdown menu, similar to the <select> HTML element. When the user taps the question, they will be presented with the native picker UI of the OS.
    * <b>gps</b> will prompt the user to confirm their current location, as determined by the device's onboard GPS.

<h3>Response</h3>

If your question is successfully created, we will respond with raw XML containing a status of 1 and the numerical ID of your new question.

Example :

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

* <b>section</b> must be set to <b>questions</b> .
* <b>action</b> must be set to <b>delete</b> .
* <b>api_key</b> must be set to (your unique API key)[../README.md#finding] .
* <b>question_id</b> - an integer or series of integers which specifies the question IDs that you wish to include in the list. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all questions.

<h3>Response</h3>

If you have successfully deleted your question, we will respond with raw XML containing a status of 1.

~~~ .xml
Example :

<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="add"></a><h2>Adding an Answer Option</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>questions</b> .
* <b>action</b> must be set to <b>addanswer</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>question_id</b> - an integer which specifies the numeric question ID you want to add an answer to.
* <b>answer_text</b> - a string which specifies the answer text you want to add to the question. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all answers.

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing an ID and status of 1.

Example: :

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

* <b>section</b> must be set to <b>questions</b> .
* <b>action</b> must be set to <b>deleteanswer</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>answer_id</b> - an integer or series of integers specifying the numerical IDs of the answers you want to remove from a question.

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing an ID and status of 1.

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~
