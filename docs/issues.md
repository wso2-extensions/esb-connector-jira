# Working with Issues in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operations are available for working with issues.Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with issues, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [getIssue](#getting-an-issue)    | Gets the specified issue. |
| [createIssue](#creating-an-issue)      | Creates a new issue.|
| [updateIssue](#updating-an-issue)      | Updates an issue. |
| [updateIssueAssignee](#assigning-an-issue-to-another-user)    | Assigns the issue to the specified user. |
| [getTransitions](#getting-transitions)      | Gets a list of transitions the current user can perform for an issue. |
| [doTransition](#performing-transitions)   | Performs a transition on an issue.|
| [getComments](#getting-comments)      | Gets the comments for an issue.|
| [postComment](#posting-a-comment)      | Posts a comment on an issue. |
| [updateComment](#updating-a-comment)    | Updates an existing comment. |
| [deleteComment](#deleting-a-comment)      | Deletes an existing comment. |
| [addAttachmentToIssueId](#adding-attachments-to-an-issue)   | Adds an attachment to an issue.|
| [getIssuePriorities](#getting-priorities)   | Gets the available priorities for issues.|
| [getIssuePriorityById](#getting-information-on-a-priority)      | Gets information about a specific priority.|
| [getIssueTypes](#getting-issue-types)      | Gets the available types of issues.|
| [getIssueTypeById](#getting-information-on-an-issue-type)    | Gets information about a specific issue type. |
| [getVotesForIssue](#getting-votes-for-an-issue)      | Gets the votes for an issue. |
| [createBulkIssue](#creating-many-issues-in-one-bulk-operation)   | Creates many issues in one bulk operation.|
| [assignIssueToUser](#assigning-an-issue-to-a-user)      | Assigns an issue to a user. |
| [getCommentById](#retrieving-all-comments-for-an-issue)   | Retrieves all comments for an issue.|
| [sendNotification](#sending-a-notification-to-the-list-or-recipients)   | Sends a notification (e-mail) to the list or recipients defined in the request.|
| [addVotesForIssue](#casting-your-vote-in-favour-of-an-issue)      | Casts your vote in favour of an issue.|
| [getWatchersForIssue](#retrieving-the-list-of-watchers-for-the-issue-with-the-given-key)      | Retrieves the list of watchers for the issue with the given key.|
| [removeUserFromWatcherList](#removing-a-user-from-an-issue-watcher-list)    | Removes a user from an issue's watcher list. |


### Operation details

Following is more information about these operations.

#### Getting an issue
To get an existing issue, use getIssue and specify the issue ID.

**getIssue**
```xml
<jira.getIssue>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <fields>{$ctx:fields}</fields>
    <expand>{$ctx:expand}</expand>
</jira.getIssue>
```
**Properties**
* issueIdOrKey: Identifies the issue to retrieve. This can be an issue ID, or an issue key.
* fields : The list of fields to return for the issue.
* expand : The parameters to expand.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getIssue operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"EX-1"
}
```
**Sample response**

Given below is a sample response for the getIssue operation.

```json
{
    "id": "10002",
    "self": "http://localhost:8080/jira/rest/api/2/issue/10002",
    "key": "EX-1",
    "fields": {
        "sub-tasks": [],
        "timetracking": {
            "originalEstimate": "10m",
            "remainingEstimate": "3m",
            "timeSpent": "6m",
            "originalEstimateSeconds": 600,
            "remainingEstimateSeconds": 200,
            "timeSpentSeconds": 400
        },
        "project": {
            "self": "http://localhost:8080/jira/rest/api/2/project/EX",
            "id": "10000",
            "key": "EX",
            "name": "Example",
            "avatarUrls": {
                "24x24": "http://localhost:8080/jira/secure/projectavatar?size=small&pid=10000",
                "16x16": "http://localhost:8080/jira/secure/projectavatar?size=xsmall&pid=10000",
                "32x32": "http://localhost:8080/jira/secure/projectavatar?size=medium&pid=10000",
                "48x48": "http://localhost:8080/jira/secure/projectavatar?size=large&pid=10000"
            }
        },
        "updated": 1,
        "description": "example bug report",
        "issuelinks": [
            {
                "id": "10001",
                "type": {
                    "id": "10000",
                    "name": "Dependent",
                    "inward": "depends on",
                    "outward": "is depended by"
                },
                "outwardIssue": {
                    "id": "10004L",
                    "key": "PRJ-2",
                    "self": "http://localhost:8080/jira/rest/api/2/issue/PRJ-2",
                    "fields": {
                        "status": {
                            "iconUrl": "http://localhost:8080/jira//images/icons/statuses/open.png",
                            "name": "Open"
                        }
                    }
                }
            }
        ],
        "attachment": [],
        "watcher": {
            "self": "http://localhost:8080/jira/rest/api/2/issue/EX-1/watchers",
            "isWatching": false,
            "watchCount": 1,
            "watchers": []
        },
        "comment": [],
        "worklog": []
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1160](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1160)

#### Creating an issue

To create a new issue (or task), use createIssue and set the following properties.

**createIssue**
```xml
<jira.createIssue>
    <projectKey>{$ctx:projectKey}</projectKey>
    <issueFields>{$ctx:issueFields}</issueFields>
</jira.createIssue>
```

**Properties**

* projectKey : The key (unique identifier) of the project in which you are creating the issue.
* issueFields: Fields of the issue.

**Sample request**

Following is a sample REST/JSON request that can be handled by the createIssue operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueFields":{
        "fields": {
            "project":{
                "key": "TEST1"
            },
            "summary": "Hello",
            "description": "test issue",
            "issuetype": {
                "id": "10000"
            }
        }
    }
}
```
**Sample response**

Given below is a sample response for the createIssue operation.

```json
{
    "id": "10000",
    "key": "TEST1",
    "self": "http://localhost:8080/jira/rest/api/2/issue/10000"
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e864](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e864)

#### Updating an issue

To update an issue, use updateIssue, specify the issue ID.

**updateIssue**
```xml
<jira.updateIssue>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <issueFields>{$ctx:issueFields}</issueFields>
</jira.updateIssue>
```
**Properties**
* issueIdOrKey: The key (unique identifier) of the issue.
* issueFields: Fields of the issue.
**Sample request**

Following is a sample REST/JSON request that can be handled by the updateIssue operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-6",
    "issueFields":{
        "update":{
            "summary":[
               {
                  "set":"Bug in business logic"
               }
            ],
            "labels":[
               {
                  "add":"triaged"
               },
               {
                  "remove":"blocker"
               }
            ]
         }
    }
}
```
**Sample response**

200 will be returned if it updated the issue succesfully.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1209](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1209)

#### Assigning an issue to another user
To assign an issue to another user, use updateIssueAssignee,  specify the issue ID.

**updateIssueAssignee**
```xml
<jira.updateIssueAssignee>
    <name>{$ctx:name}</name>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
</jira.updateIssueAssignee>
```
**Properties**
* issueIdOrKey: Identifies the issue to update. This can be an issue ID, or an issue key.
* name : The username of the user.

**Sample request**

Following is a sample request that can be handled by the updateIssueAssignee operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "name":"admin",
    "issueIdOrKey":"TEST-2"
}
```
**Sample response**

Returned 204 if the issue is successfully assigned.


**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e924](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e924)

#### Getting transitions

To get a list of the possible transitions the current user can perform for an issue, use getTransitions and  specify the issue ID.

**getTransitions**
```xml
<jira.getTransitions>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <expand>{$ctx:expand}</expand>
</jira.getTransitions>
```
**Properties**
* issueIdOrKey: Identifies the issue to update. This can be an issue ID, or an issue key.
* expand : The parameters to expand.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getTransitions operation.

```json

{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-2"
}
```
**Sample response**

Given below is a sample response for the getTransitions operation.

```json
{
    "transitions": [
        {
            "id": "2",
            "name": "Close Issue",
            "to": {
                "self": "http://localhost:8080/jira/rest/api/2.0/status/10000",
                "description": "The issue is currently being worked on.",
                "iconUrl": "http://localhost:8080/jira/images/icons/progress.gif",
                "name": "In Progress",
                "id": "10000",
                "statusCategory": {
                    "self": "http://localhost:8080/jira/rest/api/2.0/statuscategory/1",
                    "id": 1,
                    "key": "in-flight",
                    "colorName": "yellow"
                }
            },
            "fields": {...},
        {
            "id": "711",
            "name": "QA Review",
            "to": {
                "self": "http://localhost:8080/jira/rest/api/2.0/status/5",
                "description": "The issue is closed.",
                "iconUrl": "http://localhost:8080/jira/images/icons/closed.gif",
                "name": "Closed",
                "id": "5",
                "statusCategory": {
                    "self": "http://localhost:8080/jira/rest/api/2.0/statuscategory/9",
                    "id": 9,
                    "key": "completed",
                    "colorName": "green"
                }
            },
            "fields": {
                ...
            }
        }
    ]
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1074](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1074)

#### Performing transitions

To perform a transition on an issue, use doTransition, specify the issue ID, and include the transition ID along with any other updates you want to make using the following properties.

**doTransition**
```xml
<jira.doTransition>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <issueFields>{$ctx:issueFields}</issueFields>
</jira.doTransition>
```
**Properties**
* issueIdOrKey: Identifies the issue to update. This can be an issue ID, or an issue key.
* issueFields: Fields of the issue.

**Sample request**

Following is a sample request that can be handled by the doTransitions operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-2"
    "issueFields":{
     "update": {
       "comment": [
               {
                   "add": {
                       "body": "Bug has been fixed."
                       }
               }
           ]
       },
      "transition": {
           "id": "11"
       }
   }
}
```
**Sample response**

Returned 204 if the transition was successful.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1097](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1097)

#### Getting comments

To get the comments for an issue, use getComments and  specify the issue ID.

**getComments**
```xml
<jira.getComments>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <expand>{$ctx:expand}</expand>
</jira.getComments>
```
**Properties**
* issueIdOrKey: Identifies the issue whose comments you want to get. This can be an issue ID, or an issue key.
* expand: The parameters to expand.

**Sample request**

Following is a sample request that can be handled by the getComments operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-2"
}
```
**Sample response**

Given below is a sample response for the getComments operation.

```json
{
    "startAt": 0,
    "maxResults": 1,
    "total": 1,
    "comments": [
        {
            "self": "http://localhost:8080/jira/rest/api/2/issue/10010/comment/10000",
            "id": "10000",
            "author": {
                "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
                "name": "fred",
                "displayName": "Fred F. User",
                "active": false
            },
            "body": "Testing.",
            "updateAuthor": {
                "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
                "name": "fred",
                "displayName": "Fred F. User",
                "active": false
            },
            "created": "2013-08-23T16:57:35.982+0200",
            "updated": "2013-08-23T16:57:35.983+0200",
            "visibility": {
                "type": "role",
                "value": "Administrators"
            }
        }
    ]
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e957](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e957)

#### Posting a comment

To post a comment to an issue, use postComment and specify the following properties.

**postComment**
```xml
<jira.postComment>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <comment>{$ctx:comment}</comment>
    <visibleRole>{$ctx:visibleRole}</visibleRole>
    <expand>{$ctx:expand}</expand>
</jira.postComment>
```
**Properties**
* issueIdOrKey: Identifies the issue to which you are adding this comment. This can be an issue ID, or an issue key.
* Comment: The text to post as the comment.
* visibleRole: User role that can view the comment.
* expand : The parameters to expand.

**Sample request**

Following is a sample request that can be handled by the postComment operation.

```json
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-1",
    "comment":"Waiting to hear back from the legal department.",
    "visibleRole":"Administrators"
}
```
**Sample response**

Given below is a sample response for the postComment operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/issue/10010/comment/10000",
    "id": "10000",
    "author": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "displayName": "Fred F. User",
        "active": false
    },
    "body": "Testing issue",
    "updateAuthor": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "displayName": "Fred F. User",
        "active": false
    },
    "created": "2013-08-23T16:57:35.982+0200",
    "updated": "2013-08-23T16:57:35.983+0200",
    "visibility": {
        "type": "role",
        "value": "Administrators"
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e978](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e978)

#### Updating a comment

To update an existing comment, use updateComment operation.

**updateComment**
```xml
<jira.updateComment>
    <commentId>{$ctx:commentId}</commentId>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <comment>{$ctx:comment}</comment>
    <visibleRole>{$ctx:visibleRole}</visibleRole>
</jira.updateComment>
```
**Properties**
* issueIdOrKey : Identifies the issue whose comment you are updating. This can be an issue ID, or an issue key. If the issue cannot be found via an exact match, JIRA will also look for the issue in a case-insensitive way, or by looking to see if the issue was moved.
* commentId : Identifies the comment you are updating.
* comment : A string containing the comment to be posted
* visibleRole: A String containing the visible role.
* expand: The optional flags: renderedBody (provides body rendered in HTML).

**Sample request**

Following is a sample request that can be handled by the updateComment operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-1",
    "commentId":"10000",
    "comment":"is this a bug?",
    "visibleRole":"Administrators"
}
```
**Sample response**

Given below is a sample response for the updateComment operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/issue/10010/comment/10000",
    "id": "10000",
    "author": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "displayName": "Fred F. User",
        "active": false
    },
    "body": "Testing.",
    "updateAuthor": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "displayName": "Fred F. User",
        "active": false
    },
    "created": "2013-08-23T16:57:35.982+0200",
    "updated": "2013-08-23T16:57:35.983+0200",
    "visibility": {
        "type": "role",
        "value": "Administrators"
    }
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1035](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1035)

#### Deleting a comment

To delete an existing comment, use deleteComment.

**deleteComment**
```xml
<jira.deleteComment>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <commentId>{$ctx:commentId}</commentId>
</jira.deleteComment>
```
**Properties**
* issueIdOrKey: Identifies the issue whose comment you are deleting. This can be an issue ID, or an issue key.
* commentId: Identifies the comment you are deleting.

**Sample request**

Following is a sample request that can be handled by the deleteComment operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-2",
    "commentId":"10000"
}
```
**Sample response**

Returned 204 if delete is successful.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1064](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1064)

#### Adding attachments to an issue

To add one or more attachments to an issue, use addAttachmentToIssueId, specify the issue ID.

**addAttachmentToIssueId**
```xml
<jira.addAttachmentToIssueId>
  <issueIdOrKey>{$url:issueIdOrKey}</issueIdOrKey>
</jira.addAttachmentToIssueId>
```
**Properties**
* issueIdOrKey: Identifies the issue to which you are adding attachments. This can be an issue ID, or an issue key.

> NOTE: Multipart/form-data cannot be processed inside the ESB. Therefore, the ESB should be in a content-unaware status. To achieve this, configure a pass-through proxy, and then build the message from the client end and send it to the proxy.

**Sample response**

Given below is a sample response for the addAttachmentToIssueId operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2.0/attachments/10000",
        "filename": "picture.jpg",
        "author": {
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
        },
        "created": "2013-08-23T16:57:35.977+0200",
        "size": 23123,
        "mimeType": "image/jpeg",
        "content": "http://localhost:8080/jira/attachments/10000",
        "thumbnail": "http://localhost:8080/jira/secure/thumbnail/10000"
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3258](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3258)

#### Getting priorities

To get the priorities available for issues, use getIssuePriorities. This operation returns detailed information about each priority, including its name, ID, and more.

**getIssuePriorities**
```xml
<jira.getIssuePriorities/>
```

**Sample request**

Following is a sample request that can be handled by the getIssuePriorities operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080"
}
```
**Sample response**

Given below is a sample response for the getIssuePriorities operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2/priority/3",
        "statusColor": "#009900",
        "description": "Major loss of function.",
        "iconUrl": "http://localhost:8080/jira/images/icons/priorities/major.png",
        "name": "Major"
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1817](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1817)

#### Getting information on a priority

To get information on a specific priority, use getIssuePriorityById and specify the priority ID.

**getIssuePriorityById**
```xml
<jira.getIssuePriorityById>
    <issuePriorityId>{$ctx:issuePriorityId}</issuePriorityId>
</jira.getIssuePriorityById>
```
**Properties**
* issuePriorityId: Identifies the priority whose information you want to retrieve.

**Sample request**

Following is a sample request that can be handled by the getIssuePriorityById operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issuePriorityId":"3"
}
```
**Sample response**

Given below is a sample response for the getIssuePriorityById operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/priority/3",
    "statusColor": "#009900",
    "description": "Major loss of function.",
    "iconUrl": "http://localhost:8080/jira/images/icons/priorities/major.png",
    "name": "Major"
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1832](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1832)

#### Getting issue types

To get the types of issues available in this JIRA instance, use getIssueTypes. This operation returns detailed information about each issue type, including its name, ID, and more.

**getIssueTypes**
```xml
<jira.getIssueTypes/>
```

**Sample request**

Following is a sample request that can be handled by the getIssueTypes operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080"
}
```
**Sample response**

Given below is a sample response for the getIssueTypes operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2.0/issueType/3",
        "id": "3",
        "description": "A task that needs to be done.",
        "iconUrl": "http://localhost:8080/jira/images/icons/issuetypes/task.png",
        "name": "Task",
        "subtask": false
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e704](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e704)

#### Getting information on an issue type

To get information on a specific issue type, use jira.getIssueTypeById and specify the type ID.

**getIssueTypeById**
```xml
<jira.getIssueTypeById>
    <issueTypeId>{$ctx:issueTypeId}</issueTypeId>
</jira.getIssueTypeById>
```
**Properties**
* issueTypeId: Identifies the issue type whose information you want to retrieve.

**Sample request**

Following is a sample request that can be handled by the getIssueTypeById operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueTypeId":"3"
}
```
**Sample response**

Given below is a sample response for the getIssueTypeById operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2.0/issueType/3",
    "id": "3",
    "description": "A task that needs to be done.",
    "iconUrl": "http://localhost:8080/jira/images/icons/issuetypes/task.png",
    "name": "Task",
    "subtask": false
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e719](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e719)

#### Getting votes for an issue

To get the votes for a specific issue, use getVotesForIssue and specify the issue ID. This operation returns a JSON representation of the vote information, including the number of votes and more.

**getVotesForIssue**
```xml
<jira.getVotesForIssue>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
</jira.getVotesForIssue>
```
**Properties**
* issueIdOrKey: Identifies the issue whose votes you want to get. This can be an issue ID, or an issue key.

**Sample request**

Following is a sample request that can be handled by the getVotesForIssue operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-1"
}
```
**Sample response**

Given below is a sample response for the getVotesForIssue operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/issue/TEST-1/votes",
    "votes": 24,
    "hasVoted": true,
    "voters": [
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
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1143](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1143)

#### Creating many issues in one bulk operation

This operation creates many issues in one bulk operation.

**createBulkIssue**
```xml
<jira.createBulkIssue>
    <issueUpdates>{$ctx:issueUpdates}</issueUpdates>
</jira.createBulkIssue>
```
**Properties**
* issueUpdates : The array of objects containing the issue details.

**Sample request**

Following is a sample request that can be handled by the createBulkIssue operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "issueUpdates": [
        {
            "update": {},
            "fields": {
                "project": {
                    "id": "10000"
                },
                "summary": "something's very wrong",
                "issuetype": {
                    "id": "10000"
                }
            }
        }
    ]
}
```
**Sample response**

Given below is a sample response for the createBulkIssue operation.

```json
{
    "issues": [
        {
            "id": "10000",
            "key": "TST-24",
            "self": "http://localhost:8080/jira/rest/api/2/issue/10000"
        },
        {..}
    ],
    "errors": []
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1295](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1295)

#### Assigning an issue to a user

This operation assigns an issue to a user.

**assignIssueToUser**
```xml
<jira.assignIssueToUser>
    <name>{$ctx:name}</name>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
</jira.assignIssueToUser>
```
**Properties**
* issueIdOrKey:  A String containing an issue key.
* name : The name of the assignee.

**Sample request**

Following is a sample request that can be handled by the assignIssueToUser operation.

```json
{
    "uri": "https://connector.atlassian.net",
    "username": "admin",
    "password": "1qaz2wsx@",
    "name": "vrajenthiran",
    "issueIdOrKey": "WSO2CON-4"
}
```
**Sample response**

Returned 204 if the issue is successfully assigned.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e928 ](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e928 )

#### Retrieving all comments for an issue

This operation retrieves all comments for an issue.

**getCommentById**
```xml
<jira.getCommentById>
    <commentId>{$ctx:commentId}</commentId>
    <expand>{$ctx:expand}</expand>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
</jira.getCommentById>
```
**Properties**
* commentId : The unique identifier of the comment.
* expand : The optional flags: renderedBody (provides body rendered in HTML).
* issueIdOrKey : A string containing the issue ID or key the comment belongs to.

**Sample request**

Following is a sample request that can be handled by the getCommentById operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "commentId" : "10000",
    "issueIdOrKey":"TESTPM1-3"
}
```
**Sample response**

Given below is a sample response for the getCommentById operation.

```json
{
    "startAt": 0,
    "maxResults": 1,
    "total": 1,
    "comments": [
        {
            "self": "http://localhost:8080/jira/rest/api/2/issue/10010/comment/10000",
            "id": "10000",
            "author": {
                "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
                "name": "fred",
                "displayName": "Fred F. User",
                "active": false
            },
            "body": "Testing.",
            "updateAuthor": {
                "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
                "name": "fred",
                "displayName": "Fred F. User",
                "active": false
            },
            "created": "2013-08-23T16:57:35.982+0200",
            "updated": "2013-08-23T16:57:35.983+0200",
            "visibility": {
                "type": "role",
                "value": "Administrators"
            }
        }
    ]
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1014](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1014)

#### Sending a notification to the list or recipients

This operation sends a notification (e-mail) to the list or recipients defined in the request.

**sendNotification**
```xml
<jira.sendNotification>
    <subject>{$ctx:subject}</subject>
    <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
    <textBody>{$ctx:textBody}</textBody>
    <htmlBody>{$ctx:htmlBody}</htmlBody>
    <toReporter>{$ctx:toReporter}</toReporter>
    <toAssignee>{$ctx:toAssignee}</toAssignee>
    <toWatchers>{$ctx:toWatchers}</toWatchers>
    <toVoters>{$ctx:toVoters}</toVoters>
    <toUsers>{$ctx:toUsers}</toUsers>
    <toGroups>{$ctx:toGroups}</toGroups>
    <restrictGroups>{$ctx:restrictGroups}</restrictGroups>
    <restrictPermissions>{$ctx:restrictPermissions}</restrictPermissions>
</jira.sendNotification>
```
**Properties**
* subject: The subject of the notification.
* issueIdOrKey: A string containing the issue ID or key the comment will be added to.
* textBody: The text body of the notification.
* htmlBody: The HTML body of the notification.
* toReporter: The boolean flag to indicate whether to notify the reporter.
* toAssignee: The boolean flag to indicate whether to notify the assignee.
* toWatchers: The boolean flag to indicate whether to notify the watchers.
* toVoters: The boolean flag to indicate whether to notify the voters.
* toUsers: The boolean flag to indicate whether to notify the users.
* toGroups: The array of notification groups to be notified.
* restrictGroups: The Array of notification groups to be restricted.
* restrictPermissions: The array of restricted permissions for the notification.

**Sample request**

Following is a sample request that can be handled by the sendNotification operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "issueIdOrKey" : "TESTPM1-3",
    "subject" : "notification subject",
    "textBody":"The text body",
    "htmlBody":"Lorem ipsum <strong>dolor</strong> sit amet, consectetur adipiscing elit. Pellentesque eget",
    "toReporter":"false",
    "toAssignee":"false",
    "toWatchers":"true",
    "toVoters":"true",
    "toUsers":[
            {
                "name": "vrajenthiran",
                "active": false
            }
        ],
    "toGroups":[
            {
                "name": "notification-group",
                "self": "http://localhost:8080/jira/rest/api/2/group?groupname=notification-group"
            }
        ],
    "restrictPermissions":[
            {
                "id": "10",
                "key": "BROWSE"
            }
        ], "restrictGroups": [
            {
                "name": "notification-group",
                "self": "http://localhost:8080/jira/rest/api/2/group?groupname=notification-group"
            }
        ]
}
```
**Sample response**

Returned 204 if adding to the mail queue was successful.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e902](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e902)

#### Casting your vote in favour of an issue

This operation casts your vote in favour of an issue.

**addVotesForIssue**
```xml
<jira.addVotesForIssue>
    <issueId>{$ctx:issueId}</issueId>
</jira.addVotesForIssue>
```
**Properties**
* issueId : The ID of the issues that the vote is made for.

**Sample request**

Following is a sample request that can be handled by the addVotesForIssue operation.

```json
{
  "uri": "https://testappmahesh.atlassian.net",
  "username": "testapp.mahesh2",
  "password": "1qaz2wsx@",
  "issueId":"TP-1"
}
```
**Sample response**
Returned 204 if adding to the mail queue was successful.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1133](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1133)

#### Retrieving the list of watchers for the issue with the given key

This operation retrieves the list of watchers for the issue with the given key.

**getWatchersForIssue**
```xml
<jira.getWatchersForIssue>
    <issueId>{$ctx:issueId}</issueId>
</jira.getWatchersForIssue>
```
**Properties**
* issueId : The string containing an issue key.

**Sample request**

Following is a sample request that can be handled by the getWatchersForIssue operation.

```json
{
    "uri":"http://localhost:8080",
    "username":"admin",
    "password":"1qaz2wsx@",
    "issueId":"EX-1"
}
```
**Sample response**

Given below is a sample response for the getWatchersForIssue operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/issue/EX-1/watchers",
    "isWatching": false,
    "watchCount": 1,
    "watchers": [
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
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1232](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1232)

#### Removing a user from an issue watcher list

This operation removes a user from an issue's watcher list.

**removeUserFromWatcherList**
```xml
<jira.removeUserFromWatcherList>
    <name>{$ctx:name}</name>
    <issueId>{$ctx:issueId}</issueId>
</jira.removeUserFromWatcherList>
```
**Properties**
* name: String containing the name of the user to remove.
* issueId : String containing an issue key.

**Sample request**

Following is a sample request that can be handled by the removeUserFromWatcherList operation.

```json
{
    "uri":"https://connector.atlassian.net",
    "username":"admin",
    "password":"1qaz2wsx@",
    "issueId":"TESTPM1-3",
    "name" : "rasika"
}
```
**Sample response**
Returned 204 if the watcher was removed successfully.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1274 ](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1274 )

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the getComments operation.

1. Create a sample proxy as below :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxy xmlns="http://ws.apache.org/ns/synapse" name="getComments" transports="https" statistics="disable" trace="disable" startOnLoad="true">
   <target>
      <inSequence>
         <property name="uri" expression="json-eval($.uri)" />
         <property name="username" expression="json-eval($.username)" />
         <property name="password" expression="json-eval($.password)" />
         <property name="issueIdOrKey" expression="json-eval($.issueIdOrKey)" />
         <property name="expand" expression="json-eval($.expand)" />
         <jira.init>
            <uri>{$ctx:uri}</uri>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
         </jira.init>
         <jira.getComments>
            <issueIdOrKey>{$ctx:issueIdOrKey}</issueIdOrKey>
            <expand>{$ctx:expand}</expand>
         </jira.getComments>
         <respond />
      </inSequence>
      <outSequence>
         <send />
      </outSequence>
   </target>
   <description />
</proxy>
```

2. Create a json file named getComments.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "issueIdOrKey":"TEST-2"
}
```
3. Replace the credentials and details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/getComments -H "Content-Type: application/json" -d @getComments.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{
     "startAt": 0,
     "maxResults": 1,
     "total": 1,
     "comments": [
         {
             "self": "http://localhost:8080/jira/rest/api/2/issue/10010/comment/10000",
             "id": "10000",
             "author": {
                 "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
                 "name": "fred",
                 "displayName": "Fred F. User",
                 "active": false
             },
             "body": "Testing.",
             "updateAuthor": {
                 "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
                 "name": "fred",
                 "displayName": "Fred F. User",
                 "active": false
             },
             "created": "2013-08-23T16:57:35.982+0200",
             "updated": "2013-08-23T16:57:35.983+0200",
             "visibility": {
                 "type": "role",
                 "value": "Administrators"
             }
         }
     ]
 }
```
