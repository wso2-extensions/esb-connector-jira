# Working with Groups in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operation is available for working with groups.Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with groups, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [getGroup](#getting-group )    | Gets all available Jira groups. |
| [listGroupPicker](#retrieving-groups-with-substrings-matching-a-given-query)      | Retrieves groups with substrings matching a given query. |
| [listGroupUserPicker](#retrieving-a-list-of-users-and-groups-matching-query-with-highlighting)    | Retrieves a list of users and groups matching query with highlighting. |

### Operation details

Following is more information about these operations.

#### Getting group
This operation returns a JSON representation of the list of groups, including their names, IDs, and more.
**getGroup**
```xml
<jira.getGroup>
    <groupName>{$ctx:groupName}</groupName>
    <expand>{$ctx:expand}</expand>
</jira.getGroup>
```

**Properties**
* groupName: The name of the group.
* expand : The parameters to expand.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getGroup operation.
```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "groupName":"jira-administrators",
    "expand":"users"
}
```
**Sample response**

Given below is a sample response for the getGroup operation.

```json
{
    "name": "jira-administrators",
    "self": "http://localhost:8080/rest/api/2/group?groupname=jira-administrators",
    "users": {
        "size": 1,
        "items": [],
        "max-results": 50,
        "start-index": 0,
        "end-index": 0
    },
    "expand": "users"
}
```

**Related Jira Documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e2900](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e2900)

#### Retrieving groups with substrings matching a given query

This operation retrieves groups with substrings matching a given query.
**listGroupPicker**
```xml
<jira.listGroupPicker>
    <query>{$ctx:query}</query>
    <exclude>{$ctx:exclude}</exclude>
    <maxResults>{$ctx:maxResults}</maxResults>
</jira.listGroupPicker>
```
**Properties**
* query: The query to match groups against.
* exclude: The exclude from the result.
* maxResults: The max results to return.

**Sample request**

Following is a sample REST/JSON request that can be handled by the listGroupPicker operation.
```json
{
  "uri": "http://localhost:8080",
  "username": "admin",
  "password": "1qaz2wsx@",
  "query": "administrators",
  "exclude": "system-administrators",
  "maxResults": "2"
}
```
**Sample response**

Given below is a sample response for the listGroupPicker operation.

```json
{
    "header": "Showing 1 of 1 matching groups",
    "total": 1,
    "groups": [
        {
            "name": "jira-administrators",
            "html": "<b>jira-administrators</b>",
            "labels": [
                {
                    "text": "Admin",
                    "title": "Users added to this group will be given administrative access",
                    "type": "ADMIN"
                },
                {
                    "text": "Jira Software",
                    "title": "Users added to this group will be given access to <strong>Jira Software</strong>",
                    "type": "SINGLE"
                }
            ]
        }
    ]
}
```

**Related Jira Documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1689](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1689)

#### Retrieving a list of users and groups matching query with highlighting

This operation retrieves a list of users and groups matching query with highlighting.

**listGroupUserPicker**
```xml
<jira.listGroupUserPicker>
    <query>{$ctx:query}</query>
    <maxResults>{$ctx:maxResults}</maxResults>
    <isShowAvatar>{$ctx:isShowAvatar}</isShowAvatar>
</jira.listGroupUserPicker>
```
**Properties**
* query: A string used to search username, Name or e-mail address.
* maxResults: The maximum number of users to return.
* isShowAvatar: The boolean value to show avatar.

**Sample request**

Following is a sample REST/JSON request that can be handled by the listGroupUserPicker operation.
```json
{
  "uri": "http://localhost:8080",
  "username": "admin",
  "password": "1qaz2wsx@",
  "query": "admin",
  "maxResults": "1",
  "isShowAvatar": "true"
}
```
**Sample response**

Given below is a sample response for the listGroupUserPicker operation.

```json
{
    "users": {
        "users": [],
        "total": 0,
        "header": "Showing 0 of 0 matching users"
    },
    "groups": {
        "header": "Showing 1 of 1 matching groups",
        "total": 1,
        "groups": [
            {
                "name": "jira-administrators",
                "html": "jira-<b>admin</b>istrators",
                "labels": [
                    {
                        "text": "Admin",
                        "title": "Users added to this group will be given administrative access",
                        "type": "ADMIN"
                    },
                    {
                        "text": "Jira Software",
                        "title": "Users added to this group will be given access to <strong>Jira Software</strong>",
                        "type": "SINGLE"
                    }
                ]
            }
        ]
    }
}
```

**Related Jira Documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e776](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e776)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the getGroup operation. You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :

```xml
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="getGroup"
       transports="https http"
       startOnLoad="true"
       trace="disable">
   <description/>
   <target>
      <inSequence>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="groupName" expression="json-eval($.groupName)"/>
         <property name="expand" expression="json-eval($.expand)"/>
         <jira.init>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <uri>{$ctx:uri}</uri>
         </jira.init>
         <jira.getGroup>
            <groupName>{$ctx:groupName}</groupName>
        <expand>{$ctx:expand}</expand>
         </jira.getGroup>
         <log level="full"/>
         <respond/>
      </inSequence>
      <outSequence/>
      <faultSequence/>
   </target>
</proxy>
```

2. Create a json file named getGroup.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "groupName":"jira-administrators",
    "expand":"users"
}
```
3. Replace the credentials and the details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/getGroup -H "Content-Type: application/json" -d @getGroup.json
```

5. Jira returns a json response similar to the one shown below:
 
```json
{
    "name": "jira-administrators",
    "self": "http://localhost:8080/rest/api/2/group?groupname=jira-administrators",
    "users": {
        "size": 1,
        "items": [],
        "max-results": 50,
        "start-index": 0,
        "end-index": 0
    },
    "expand": "users"
}
```
