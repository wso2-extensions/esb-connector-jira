# Working with Issue Links in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 
The following operations allow you to work with issue links. Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with issue links, see [Sample configuration](#sample-configuration).


| Operation        | Description |
| ------------- |-------------|
| [createIssueLink](#creating-an-issue-link-between-two-issues)    | 	Creates an issue link between two issues. |
| [getIssueLinkById](#retrieving-an-issue-link-with-the-specified-ID)      | Retrieves an issue link with the specified ID. |

### Operation details

This section provides further details on the operations related to issue links.

#### Creating an issue link between two issues

The createIssueLink operation creates an issue link between two issues.

**createIssueLink**
```xml
<jira.createIssueLink>
    <typeName>{$ctx:typeName}</typeName>
    <inwardIssueKey>{$ctx:inwardIssueKey}</inwardIssueKey>
    <outwardIssueKey>{$ctx:outwardIssueKey}</outwardIssueKey>
    <commentBody>{$ctx:commentBody}</commentBody>
    <commentVisibility>{$ctx:commentVisibility}</commentVisibility>
</jira.createIssueLink>
```

**Properties**

* typeName: Name of the issue type.
* inwardIssueKey: Key of the inward issue.
* outwardIssueKey: Key of the outward issue.
* commentBody: Body of the comment.
* commentVisibility: Visibility of the comment.

**Sample request**

Following is a sample REST/JSON request that can be handled by the createIssueLink operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "typeName": "Duplicate",
    "inwardIssueKey": "TESTPM1-1",
    "outwardIssueKey": "TESTPM1-2",
    "commentBody": "Linked related issue!",
    "commentVisibility": {
        "type": "group",
        "value": "jira-users"
    }
}
```
**Sample response**

As a successful response you will get 201 status code without any response body.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1898](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1898)

#### Retrieving an issue link with the specified ID

The getIssueLinkById operation retrieves an issue link with the specified ID.

**getIssueLinkById**
```xml
<jira.getIssueLinkById>
    <linkId>{$ctx:linkId}</linkId>
</jira.getIssueLinkById>
```
**Properties**
* linkId: The issue link ID.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getIssueLinkById operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "linkId": "10000"
}
```
**Sample response**

Given below is a sample response for the getIssueLinkById operation.

```json
{
    "id": "10000",
    "self": "http://localhost:8080/rest/api/2/issueLink/10000",
    "type": {
        "id": "10002",
        "name": "Duplicate",
        "inward": "is duplicated by",
        "outward": "duplicates",
        "self": "http://localhost:8080/rest/api/2/issueLinkType/10002"
    },
    "inwardIssue": {
        "id": "10002",
        "key": "KANA-3",
        "self": "http://localhost:8080/rest/api/2/issue/10002",
        "fields": {
            "summary": "New task",
            "status": {
                "self": "http://localhost:8080/rest/api/2/status/10000",
                "description": "",
                "iconUrl": "http://localhost:8080/",
                "name": "To Do",
                "id": "10000",
                "statusCategory": {
                    "self": "http://localhost:8080/rest/api/2/statuscategory/2",
                    "id": 2,
                    "key": "new",
                    "colorName": "blue-gray",
                    "name": "To Do"
                }
            },
            "priority": {
                "self": "http://localhost:8080/rest/api/2/priority/3",
                "iconUrl": "http://localhost:8080/images/icons/priorities/medium.svg",
                "name": "Medium",
                "id": "3"
            },
            "issuetype": {
                "self": "http://localhost:8080/rest/api/2/issuetype/10003",
                "id": "10003",
                "description": "A task that needs to be done.",
                "iconUrl": "http://localhost:8080/secure/viewavatar?size=xsmall&avatarId=10318&avatarType=issuetype",
                "name": "Task",
                "subtask": false,
                "avatarId": 10318
            }
        }
    },
    "outwardIssue": {
        "id": "10001",
        "key": "KANA-2",
        "self": "http://localhost:8080/rest/api/2/issue/10001",
        "fields": {
            "summary": "Framework IMplementation",
            "status": {
                "self": "http://localhost:8080/rest/api/2/status/10000",
                "description": "",
                "iconUrl": "http://localhost:8080/",
                "name": "To Do",
                "id": "10000",
                "statusCategory": {
                    "self": "http://localhost:8080/rest/api/2/statuscategory/2",
                    "id": 2,
                    "key": "new",
                    "colorName": "blue-gray",
                    "name": "To Do"
                }
            },
            "priority": {
                "self": "http://localhost:8080/rest/api/2/priority/3",
                "iconUrl": "http://localhost:8080/images/icons/priorities/medium.svg",
                "name": "Medium",
                "id": "3"
            },
            "issuetype": {
                "self": "http://localhost:8080/rest/api/2/issuetype/10003",
                "id": "10003",
                "description": "A task that needs to be done.",
                "iconUrl": "http://localhost:8080/secure/viewavatar?size=xsmall&avatarId=10318&avatarType=issuetype",
                "name": "Task",
                "subtask": false,
                "avatarId": 10318
            }
        }
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/5.0.html#id199057](https://developer.atlassian.com/static/rest/jira/5.0.html#id199057)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to JIRA with the init operation and use the createIssueLink operation.

1. Create a sample proxy as below :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxy xmlns="http://ws.apache.org/ns/synapse" name="jira_createIssueLink" transports="https" statistics="disable" trace="disable" startOnLoad="true">
   <target>
      <inSequence>
         <property name="uri" expression="json-eval($.uri)" />
         <property name="username" expression="json-eval($.username)" />
         <property name="password" expression="json-eval($.password)" />
         <property name="typeName" expression="json-eval($.typeName)" />
         <property name="inwardIssueKey" expression="json-eval($.inwardIssueKey)" />
         <property name="outwardIssueKey" expression="json-eval($.outwardIssueKey)" />
         <property name="commentBody" expression="json-eval($.commentBody)" />
         <property name="commentVisibility" expression="json-eval($.commentVisibility)" />
         <jira.init>
            <uri>{$ctx:uri}</uri>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
         </jira.init>
         <jira.createIssueLink>
            <typeName>{$ctx:typeName}</typeName>
            <inwardIssueKey>{$ctx:inwardIssueKey}</inwardIssueKey>
            <outwardIssueKey>{$ctx:outwardIssueKey}</outwardIssueKey>
            <commentBody>{$ctx:commentBody}</commentBody>
            <commentVisibility>{$ctx:commentVisibility}</commentVisibility>
         </jira.createIssueLink>
         <respond />
      </inSequence>
      <outSequence>
         <send />
      </outSequence>
   </target>
   <description />
</proxy>
```

2. Create a json file named jira_createIssueLink.json and copy the configurations given below to it:

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "typeName": "Duplicate",
    "inwardIssueKey": "TESTPM1-1",
    "outwardIssueKey": "TESTPM1-2",
    "commentBody": "Linked related issue!",
    "commentVisibility": {
        "type": "group",
        "value": "jira-users"
    }
}
```
3. Replace the credentials and the details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/jira_createIssueLink -H "Content-Type: application/json" -d @jira_createIssueLink.json
```
5. Jira returns 201 as successful response for this request.
