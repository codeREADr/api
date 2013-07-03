<a name="head"></a><h1>API: Error Codes</h1>

Error codes generated when performing an API action will display in the <b><status></b> node of the XML response.

Example:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1001</id>
</xml>
~~~

<h2>Possible Error Codes</h2>

| ID | Error Description |
|----|-------------------|
| 2  |     Your request could not be processed at this time. Our team has been notified of the issue, and you will receive a reply from us shortly. |
| 10 | No permissions for this action |
| 50 | Required POST variables not supplied |
| 100 |    The API key is invalid. |
| 101 |    The API key is missing. |
| 102 |    The XML file is too large. Maximum file size is 1MB. |
| 103 |    The XML file contains errors and cannot be read. |
| 104 |    No file has been received. Try specifying MAX_FILE_SIZE=1000000before submitting the file. |
| 105 |    The file is larger than allowed. |
| 110 |    Invalid action Parameter |
| 120 |    Invalid section Parameter |
| 131 |    Missing required variable: service_id |
| 132 |    Missing required variable: user_id |
| 133 |    Missing required variable: question_id |
| 134 |    Missing required variable: answer_id |
| 135 |    Missing required variable: scan_id |
| 200 |    The service does not exist. |
| 201 |    The user does not exist. |
| 202 |    The question does not exist. |
| 203 |    The answer does not exist. |
| 204 |    The database does not exist. |
| 205 |    This database cannot be deleted because it is currently linked to one or more services. Unlink those services from the database and try again. |
| 206 |    Cannot delete. The question must have at least two answers to choose from. |
| 210 |    Required service POST variables not supplied |
| 211 |    For database services, please select a database to be used with the service. |
| 213 |    You need to select an end date that occurs after the start date. |
| 214 |    Your stop date must be in the future. |
| 215 |    A service already exists with that name. |
| 216 |    A database already exists with that name. |
| 217 |    You need to specify a start date. |
| 218 |    You need to specify an end date. |
| 219 |    Service name is invalid |
| 221 |    Please enter a valid Postback URL, starting with http:// or https:// |
| 261 |    Question could not be deleted |
| 262 |    Invalid Question ID |
| 265 |    Answer could not be added |
| 266 |    Answer could not be deleted |
| 269 |    You need to supply a question. |
| 270 |    Invalid database ID |
| 300 |    Invalid user ID |
| 310 |    Required user POST variables not supplied |
| 320 |    The username you chose is already taken. Please choose a different username. |
| 330 |    Please enter a valid email address. |
| 340 |    Invalid username. Try taking out any spaces, or using fewer punctuation marks. |
| 341 |    Please enter a password. |
| 342 |    Please enter a username. |
| 410 |    Required device POST variables not supplied |
| 804 |    The scan could not be deleted. |
| 1017 |    Barcode value does not exist. |
| 1019 |    An error occurred during file upload. Please reattempt. |
| 1026 |   Please select a .CSV file to import. |
| 1027 |   The barcode value already exists within this database. |
| 1028 |   You need to supply a barcode value. |
| 1029 |   Please supply a CSV file to upload. |
| 1036 |   Some of the answers match. Please provide unique answers. |

<a name="head">Back to Top</a>
