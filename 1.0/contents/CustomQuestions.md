# codeREADr Custom Questions<a name="head"></a>
Custom Questions are a way for developers to code their own question types tailored to collect and validate answer data using HTML and Javascript.

## Implementation<a name="implement"></a>
Concept is simply adding a few javascript functions to your own web page for sending, receiving and validating the current answer state of your question.

>#### Offline Limitations
This may go without saying but for your question to work offline it cannot be dependent on any remote resources (i.e. jquery libraries, images, etc) and the question should be created with the HTML (i.e. source code) option instead of the URL option.

#### Required Javascript Functions

##### ```getAnswerForCR()```
&nbsp;&nbsp;&nbsp;&nbsp; Returns the current answer ```VALUE``` string. This is where you can do calculations, formatting, etc. to ready the answer for collection.

##### ```setAnswerForCR(VALUE)```
&nbsp;&nbsp;&nbsp;&nbsp; This function is responsible receiving the answer ```VALUE``` from the app and loading it into your Custom Question UI.

##### ```fireAnswerForCR()```
&nbsp;&nbsp;&nbsp;&nbsp; Sends the answer to the app by firing a location load event (i.e. ```window.location = codereadr:answerForCR:NEW_ANSWER_VALUE```) that the app will consume. You do not have to modify this function but it should be called anytime the answer value changes or to set a default answer.

##### ```isAnswerValidForCR()```
&nbsp;&nbsp;&nbsp;&nbsp; A boolean function that returns false if the current answer is invalid and should prevent the user from submitting the scan. By default you should return `true`. Only return `false` if you are validating the answer and want to block scan submit when the answer is not valid.

## Example<a name="example"></a>
Below is a barebones zip code custom question. (An extend version: <a href="https://github.com/codeREADr/api/blob/master/1.0/contents/examples/webcollect/zipcode.html" target="_blank">View</a> or <a href="https://raw.github.com/codeREADr/api/master/1.0/contents/examples/webcollect/zipcode.html" target="_blank">Download</a>)

```html
<html>
<head>
<title>Zip Code Question</title>
  <script type="text/javascript">

 // Regular expression for validating zip code format.
 var postalCodeRegExp = new RegExp("^\\d{5}(-\\d{4})?$");

 // The app calls this to overwrite the current answer with a saved answer.
 function setAnswerForCR(the_answer) {
    document.getElementById("zipcode").value = the_answer;
 }

 // The app and fireAnswerForCR calls this to get the current answer.
 function getAnswerForCR() {
    return document.getElementById("zipcode").value;
 }

 // Sends the answer to the app. It should be called anytime the answer changes.
 function fireAnswerForCR() {
    window.location = "codereadr:answerForCR:" + getAnswerForCR();
 }

 // Tests the current answer input for a regular expression match.
 function isAnswerValidForCR() {
    var the_answer = document.getElementById("zipcode").value;
    var isValid = postalCodeRegExp.test(the_answer);
    return isValid;
 }

  </script>
  </head>
  <body>
    <!-- We call fireAnswerForCR anytime the input changes. -->
    <input type="text" id="zipcode" oninput="fireAnswerForCR()" />
  </body>
</html>
```

## Creating with API<a name="create"></a>
You will either be creating the question by supplying a URL to the question page or the actual source code of the question page.
 - <a href="Questions.md#create">Create a question</a> of type `webcollect` and keep track of the returned codeREADr question ID. <br/> ```https://api.codereadr.com/api/?section=questions&action=create&question_text=YOUR_QUESTION_LABEL&api_key=YOUR_API_KEY```
 - <a href="Questions.md#add">Add an answer option</a> to the question by setting `question_id` to the returned ID and setting the `answer_text` to either your implementation's URL wrapped in a `curl` tag or the HTML source code directly. <br/> ```https://api.codereadr.com/api/?section=questions&action=addanswer&question_id=RETURNED_ID&```**```answer_text=<curl>http://example.com/custom_question.html</curl>```**```&api_key=YOUR_API_KEY``` <br/> OR <br/> ```https://api.codereadr.com/api/?section=questions&action=addanswer&question_id=RETURNED_ID&```**```answer_text=<html><head>...</head></html>```**```&api_key=YOUR_API_KEY```

<br/><br/>
