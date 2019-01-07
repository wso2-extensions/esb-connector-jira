# Working with Users in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operations are available for working with users.Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with users, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [getUser](#getting-information-on-a-user)    | Gets information for the specified user. |
| [getUserPermissions](#getting-the-current-user-permissions)      | Gets the permissions for the current user. |
| [searchUser](#searching-for-users )      | Gets a list of users that match a search string. |
| [searchIssueViewableUsers](#searching-for-users-who-can-view-an-issue-or-project )      | Gets a list of users that match a search string and have permission to view the specified issue or project. |
| [searchAssignableUser](#searching-for-users-who-can-be-assigned-to-an-issue )      | Gets a list of users that match a search string and can be assigned the specified issue. |
### Operation details

Following is more information about these operations.

#### Getting information on a user
To get information about a specified user, use getUser and specify the username.

**getUser**
```xml
<jira.getUser>
    <usernameFilter>{$ctx:usernameFilter}</usernameFilter>
    <key>{$ctx:key}</key>
</jira.getUser>
```

**Properties**

* usernameFilter : Identifies the user whose information you want to get.
* key : The user key.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getUser operation.
```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "usernameFilter":"fred"
}
```
**Sample response**

Given below is a sample response for the getUser operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
    "name": "fred",
    "emailAddress": "fred@example.com",
    "avatarUrls": {
        "24x24": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
        "16x16": "http://localhost:8080/jira/secure/useravatar?size=xsmall&ownerId=fred",
        "32x32": "http://localhost:8080/jira/secure/useravatar?size=medium&ownerId=fred",
        "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
    },
    "displayName": "Fred F. User",
    "active": true,
    "timeZone": "Australia/Sydney",
    "groups": {
        "size": 3,
        "items": []
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3476](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3476)

#### Getting the current user permissions

To get information on the current user's permissions, use getUserPermissions. You can optionally provide a specific context for which you want to get permissions (projectKey OR projectId OR issueKey OR issueId).

**getUserPermissions**
```xml
<jira.getUserPermissions>
    <projectKey>{$ctx:projectKey}</projectKey>
    <projectId>{$ctx:projectId}</projectId>
    <issueKey>{$ctx:issueKey}</issueKey>
    <issueId>{$ctx:issueId}</issueId>
</jira.getUserPermissions>
```
**Properties**
* projectKey or projectId :  Identifies the project for which you want to determine the current user's permissions.
* issueKey or issueId :  Identifies the issue for which you want to determine the current user's permissions.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getUserPermissions operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the getUserPermissions operation.

```json
{
    "permissions": {
        "EDIT_ISSUE": {
            "id": "12",
            "key": "EDIT_ISSUE",
            "name": "Edit Issues",
            "description": "Ability to edit issues.",
            "havePermission": true
        }
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e2687](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e2687)

#### Searching for users

To search for users whose username, name, or email address match a search string, use jira.searchUser and specify the search string.

**searchUser**
```xml
<jira.searchUser>
    <usernameForSearch>{$ctx:usernameForSearch}</usernameForSearch>
    <startAt>{$ctx:startAt}</startAt>
    <maxResults>{$ctx:maxResults}</maxResults>
    <includeActive>{$ctx:includeActive}</includeActive>
    <includeInactive>{$ctx:includeInactive}</includeInactive>
</jira.searchUser>
```
**Properties**
* usernameForSearch: The search string used to search the username, name, or email address.
* startAt: Optional. The 0-based index of the first user to return (default is 0).
* maxResults: Optional. The maximum number of users to return, up to 1000 (default is 50).
* includeActive: Optional. Whether to return active users (default is true).
* includeInactive: Optional. Whether to return inactive users (default is false).

**Sample request**

Following is a sample REST/JSON request that can be handled by the searchUser operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "usernameForSearch":"fred"
}
```
**Sample response**

Given below is a sample response for the searchUser operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "avatarUrls": {
            "24x24": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=xsmall&ownerId=fred",
            "32x32": "http://localhost:8080/jira/secure/useravatar?size=medium&ownerId=fred",
            "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
        },
        "displayName": "Fred F. User",
        "active": false
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3757](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3757)

#### Searching for users who can view an issue or project

To search for users whose username, name, or email address match a search string and have permission to view the specified issue or project, use searchIssueViewableUsers and specify the search string and issue key or project key.

**searchIssueViewableUsers**
```xml
<jira.searchIssueViewableUsers>
    <usernameForSearch>{$ctx:usernameForSearch}</usernameForSearch>
    <issueKey>{$ctx:issueKey}</issueKey>
    <projectKey>{$ctx:projectKey}</projectKey>
    <startAt>{$ctx:startAt}</startAt>
    <maxResults>{$ctx:maxResults}</maxResults>
</jira.searchIssueViewableUsers>
```
**Properties**
* username: The search string used to search the username, name, or email address.
* issueKey: Identifies the issue that users must have permission to view to be included in the results.
* projectKey: If you want to search for users who can browse a project instead of a specific issue, specify projectKey instead of issueKey.
* startAt: Optional. The 0-based index of the first user to return (default is 0).
* maxResults: Optional. The maximum number of users to return, up to 1000 (default is 50).

**Sample request**

Following is a sample REST/JSON request that can be handled by the searchIssueViewableUsers operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "usernameForSearch":"fred",
    "projectKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the searchIssueViewableUsers operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "avatarUrls": {
            "24x24": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=xsmall&ownerId=fred",
            "32x32": "http://localhost:8080/jira/secure/useravatar?size=medium&ownerId=fred",
            "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
        },
        "displayName": "Fred F. User",
        "active": false
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3887](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3887)

#### Searching for users who can be assigned to an issue

To search for users whose username, name, or email address match a search string and can be assigned to a specific issue, use searchAssignableUser. You specify the search string and either the project key (if getting users for a new issue you are creating) or the issue key (if getting users for an existing issue you are editing).

**searchAssignableUser**
```xml
<jira.searchAssignableUser>
    <usernameForSearch>{$ctx:usernameForSearch}</usernameForSearch>
    <project>{$ctx:project}</project>
    <issueKey>{$ctx:issueKey}</issueKey>
    <startAt>{$ctx:startAt}</startAt>
    <maxResults>{$ctx:maxResults}</maxResults>
    <actionDescriptorId>{$ctx:actionDescriptorId}</actionDescriptorId>
</jira.searchAssignableUser>
```
**Properties**
* usernameForSearch: The search string used to search the username, name, or email address.
* project: Identifies the project in which you are creating a new issue and want to get a list of users who can be assigned to it.
* issueKey: Identifies the issue you are editing so you can get a list of users who can be assigned to it.
* startAt: Optional. The 0-based index of the first user to return (default is 0).
* maxResults: Optional. The maximum number of users to return, up to 1000 (default is 50).
* actionDescriptorId: Optional.The id of the workflow action.

**Sample request**

Following is a sample REST/JSON request that can be handled by the searchAssignableUser operation.
```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the searchAssignableUser operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
    "name": "fred",
    "emailAddress": "fred@example.com",
    "avatarUrls": {
        "24x24": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
        "16x16": "http://localhost:8080/jira/secure/useravatar?size=xsmall&ownerId=fred",
        "32x32": "http://localhost:8080/jira/secure/useravatar?size=medium&ownerId=fred",
        "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
    },
    "displayName": "Fred F. User",
    "active": true,
    "timeZone": "Australia/Sydney",
    "groups": {
        "size": 3,
        "items": []
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3823](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3823)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the getUser operation.  You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :

```xml
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="getUser"
       transports="https http"
       startOnLoad="true"
       trace="disable">
   <description/>
   <target>
      <inSequence>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="usernameFilter" expression="json-eval($.usernameFilter)"/>
         <property name="key" expression="json-eval($.key)"/>
         <jira.init>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <uri>{$ctx:uri}</uri>
         </jira.init>
         <jira.getUser>
            <usernameFilter>{$ctx:usernameFilter}</usernameFilter>
            <key>{$ctx:key}</key>
         </jira.getUser>
         <log level="full"/>
         <respond/>
      </inSequence>
      <outSequence/>
      <faultSequence/>
   </target>
</proxy>
```

2. Create a json file named getUser.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "usernameFilter":"fred"
}
```
3. Replace the credentials and the details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/getUser -H "Content-Type: application/json" -d @getUser.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{
    "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
    "name": "fred",
    "emailAddress": "fred@example.com",
    "avatarUrls": {
        "24x24": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
        "16x16": "http://localhost:8080/jira/secure/useravatar?size=xsmall&ownerId=fred",
        "32x32": "http://localhost:8080/jira/secure/useravatar?size=medium&ownerId=fred",
        "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
    },
    "displayName": "Fred F. User",
    "active": true,
    "timeZone": "Australia/Sydney",
    "groups": {
        "size": 3,
        "items": []
    }
}
```
