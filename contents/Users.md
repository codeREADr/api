<a name="head"></a><h1>API: Users</h1>

<a name="retrieve"></a><h2>Retrieving a List of Users</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>users</b> .
* <b>action</b> must be set to <b>retrieve</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .

<h3>Optional Variables</h3>

* <b>user_id</b> - an integer or set of integers specifying the user IDs you would like us to list. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to include all users. This parameter is set to <b>all</b> by default.

<h3>Response</h3>

After we receive these variables, we will respond with raw XML containing status and user information, including authorized services for each user.

Example :

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

* <b>section</b> must be set to <b>users</b> .
* <b>action</b> must be set to <b>create</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>username</b> - a string which specifies the name of your new user. We will return an error code if the username already exists in the system.
* <b>password</b> - a string which specifies the password of your new user.

<h3>Optional Variables</h3>

* <b>limit</b> - an integer which specifies the maximum number of devices the user can activate during a billing period. A new user can activate an unlimited number of devices by default.

<h3>Response</h3>

If a new user is successfully created after we receive these variables, we will respond with raw XML containing a status of 1 and your new user's ID.

Example :

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

* <b>section</b> must be set to <b>users</b> .
* <b>action</b> must be set to <b>update</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>user_id</b> - an integer which specifies the user ID you wish to edit.

<h3>Optional Variables</h3>

* <b>username</b> - a string which specifies what you'd like to rename the user. We will return an error code if the new username already exists in the system.
* <b>password</b> - a string which specifies the new password for the user.
* <b>limit</b> - an integer which specifies the maximum number of devices the user can activate during a billing period. A new user can activate an unlimited number of devices by default.

<h3>Response</h3>

If the user you specified is successfully edited after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)

<a name="delete"></a><h2>Deleting a User</h2>

<h3>Required Variables</h3>

* <b>section</b> must be set to <b>users</b> .
* <b>action</b> must be set to <b>delete</b> .
* <b>api_key</b> must be set to [your unique API key](../README.md#finding) .
* <b>user_id</b> - an integer or set of integers which specify the user IDs you wish to delete. You can specify a single integer or a comma-separated list of integers ( Examples : 1005 or 1005, 1010, 1254 ). You can also use the keyword <b>all</b> to delete all users.

<h3>Response</h3>

If the users you specified are successfully deleted after we receive these variables, we will respond with raw XML containing a status of 1.

Example :

~~~ .xml
<?xml version="1.0" encoding="UTF-8"?>
<xml>
    <status>1</status>
</xml>
~~~

[Back to Top](#head)
