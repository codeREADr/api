<a name="head"></a><h1>API: Users</h1>

Make sure to read the [API Overview](https://www.codereadr.com/apidocs/README.md) before reading this document.

<a name="retrieve"></a><h2>Retrieving a List of Users</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>users</code>. |
| action | Must be set to <code>retrieve</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |

<h3>Optional Variables</h3>

| Variables | Description |
| --------- | ----------- |
| user_id | An integer or set of integers specifying the user IDs you would like us to list. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to include all users. This parameter is set to <code>all</code> by default. |

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and user information, including authorized services for each user.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <user id="73">
        <username>John</username>
        <service id="1234"/>
        <service id="1235"/>
        <service id="1236"/>
        <limit>10</limit>
        <created>2009-11-30 11:28:20</created>
    </user>
</xml>
~~~

[Back to Top](#head)

<a name="create"></a><h2>Creating a User</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>users</code>. |
| action | Must be set to <code>create</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| username | A string that specifies the identifying name of the new user. <br> Note: If the '__username__' is an email address, the '__password__' variable is ignored because the user will be required to set their own password.|
| password | _(Conditionally Required)_ A string that specifies the password for the new user. <br> Note: If the username is __not__ an email address, the '__password__' variable is required.|

<h3>Optional Variables</h3>

| Variables | Description |
| --------- | ----------- |
| limit | An integer which specifies the maximum number of devices the user can activate during a billing period. A new user can activate an unlimited number of devices by default. |

<h3>Response</h3>

If a new user is successfully created after receiving your request, we will respond with raw XML containing a status of <code>1</code> and the new user's ID. Additionally, if the username is an email address, an invitation email will be sent to the user. The user will only be able to log in and use the system after accepting the invitation.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <id>1001</id>
</xml>
~~~

[Back to Top](#head)

<a name="edit"></a><h2>Editing a User</h2>

Variables omitted when editing a user will not affect the variable's correspondent user settings.

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>users</code>. |
| action | Must be set to <code>update</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| user_id | An integer which specifies the user ID you wish to edit. |

<h3>Optional Variables</h3>

| Variables | Description |
| --------- | ----------- |
| username | A string which specifies what you'd like to rename the user. We will return an error code if the new username already exists in the system. |
| password | A string which specifies the new password for the user. |
| limit | An integer which specifies the maximum number of devices the user can activate during a billing period. A new user can activate an unlimited number of devices by default. |

<h3>Response</h3>

If the user you specified is successfully edited after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="delete"></a><h2>Deleting a User</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>users</code>. |
| action | Must be set to <code>delete</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| user_id | An integer or set of integers which specify the user IDs you wish to delete. You can specify a single integer or a comma-separated list of integers (Examples: <code>1005</code> or <code>1005, 1010, 1254</code>). You can also use the keyword <code>all</code> to delete all users. |

<h3>Response</h3>

If the users you specified are successfully deleted after we receive these variables, we will respond with raw XML containing a status of <code>1</code>.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="validate"></a><h2>Validating a User</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>users</code>. |
| action | Must be set to <code>validate</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| username | A string which specifies the username of the user to validate |
| password | A string which specifies the password of the user to validate. |

<h3>Response</h3>

After we receive these variables and if credentials are valid, we will respond with raw XML containing status and user information, including authorized services the user.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
    <user id="73">
        <username>John</username>
        <service id="1234"/>
        <service id="1235"/>
        <service id="1236"/>
        <limit>10</limit>
        <created>2009-11-30 11:28:20</created>
    </user>
</xml>
~~~

[Back to Top](#head)
<!---
<a name="available"></a><h2>Username Availability</h2>

<h3>Required Variables</h3>

| Variables | Description |
| --------- | ----------- |
| section | Must be set to <code>users</code>. |
| action | Must be set to <code>available</code>. |
| api_key | Must be set to [your unique API key](https://www.codereadr.com/apidocs/README.md#finding). |
| username | A string which specifies the username to check for availability. |

<h3>Response</h3>

After we receive these variables we will respond with raw XML containing status <code>1</code> if <i>username</i> is available and <code>0</code> if it is not available.

*Example*:

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)
-->
