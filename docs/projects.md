# Working with Projects in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operations are available for working with projects.Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with projects, see [Sample configuration](#sample-configuration).


| Operation        | Description |
| ------------- |-------------|
| [getProject](#getting-information-about-a-project)    | Gets information about a project. |
| [getAvatarsForProject](#getting-avatars-for-a-project)      | Gets all avatars available for a project that are visible to the current user.|
| [deleteAvatarForProject](#deleting-an-avatar-from-a-project)      | Deletes an avatar from a project. |
| [getComponentsOfProject](#getting-components-of-a-project)    | Gets all the components of a project. |
| [getStatusesOfProject](#getting-statuses-of-a-project)      | Gets the issue types and their valid status values for a project. |
| [getVersionsOfProject](#getting-versions-of-a-project)   | Gets all the versions of a project.|
| [getRolesOfProject](#getting-roles-of-a-project)   | Gets all the roles in a project.|
| [getRolesByIdOfProject](#getting-information-on-a-role)   | Gets details on a specific role.|
| [getUserAssignableProjects](#returns-a-list-of-users-can-be-assigned-issues-for-all-the-given-projects)   | Gets a list of users that match the search string.|
| [setActorsToRoleOfProject](#assigning-users-to-a-role)   | Assigns users to a role in a project.|

### Operation details

Following is more information about these operations.

#### Getting information about a project
To get information about a specific project, use getProject and specify the project key. This operation returns a JSON representation of the entire project, including name, ID, components, and more.

**getProject**
```xml
<jira.getProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
    <expand>{$ctx:expand}</expand>
</jira.getProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.
* expand : The parameters to expand.

**Sample request**

Following is a sample request that can be handled by the getProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"EX"
}
```
**Sample response**

Given below is a sample response for the getProject operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/project/EX",
    "id": "10000",
    "key": "EX",
    "description": "This project was created as an example for REST.",
    "lead": {
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
    "components": [
        {
            "self": "http://localhost:8080/jira/rest/api/2/component/10000",
            "id": "10000",
            "name": "Component 1",
            "description": "This is a JIRA component",
            "lead": {
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
            "assigneeType": "PROJECT_LEAD",
            "assignee": {
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
            "realAssigneeType": "PROJECT_LEAD",
            "realAssignee": {
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
            "isAssigneeTypeValid": false
        }
    ],
   ..
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3008](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3008)

#### Getting avatars for a project

To get the avatars available for a specific project, use getAvatarsForProject and specify the project key. This operation returns a JSON representation of the avatars, including their name, ID, and whether the avatar is currently selected for the project.

**getAvatarsForProject**
```xml
<jira.getAvatarsForProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
</jira.getAvatarsForProject>
```

**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.

**Sample request**

Following is a sample request that can be handled by the getAvatarsForProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the getAvatarsForProject operation.

```json
{
    "system": [
        {
            "id": "1000",
            "owner": "fred",
            "isSystemAvatar": true,
            "isSelected": true,
            "selected": true
        }
    ],
    "custom": [
        {
            "id": "1010",
            "owner": "andrew",
            "isSystemAvatar": false,
            "isSelected": false,
            "selected": false
        }
    ]
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3151](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3151)

#### Deleting an avatar from a project

To delete an avatar from a project, use deleteAvatarForProject and specify the project key and avatar ID.

**deleteAvatarForProject**
```xml
<jira.deleteAvatarForProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
    <avatarId>{$ctx:avatarId}</avatarId>
</jira.deleteAvatarForProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.
* avatarId: Identifies the avatar to delete.

**Sample request**

Following is a sample request that can be handled by the deleteAvatarForProject operation.

```json
{
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST",
    "avatarId":"10412"
}
```
**Sample response**

204 will returned if the avatar is successfully deleted.

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3175](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3175)

#### Getting components of a project
To get the components of a specific project, use getComponentsOfProject and specify the project key. This operation returns a JSON representation of the components, including their name, ID, and avatars.

**getComponentsOfProject**
```xml
<jira.getComponentsOfProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
</jira.getComponentsOfProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.

**Sample request**

Following is a sample request that can be handled by the getComponentsOfProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the getComponentsOfProject operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2/component/10000",
        "id": "10000",
        "name": "Component 1",
        "description": "This is a JIRA component",
        "lead": {
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
        "assigneeType": "PROJECT_LEAD",
        "assignee": {
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
        "realAssigneeType": "PROJECT_LEAD",
        "realAssignee": {
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
        "isAssigneeTypeValid": false
    },
   ...
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3218](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3218)

#### Getting statuses of a project

To get the statuses of a specific project, usegetStatusesOfProject and specify the project key. This operation returns a JSON representation of each issue type in the project and their statuses.

**getStatusesOfProject**
```xml
<jira.getStatusesOfProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
</jira.getStatusesOfProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.

**Sample request**

Following is a sample request that can be handled by the getStatusesOfProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the getStatusesOfProject operation.

```json
[
    {
        "self": "http://localhost:8090/jira/rest/api/2.0/issueType/3",
        "id": "3",
        "name": "Task",
        "subtask": false,
        "statuses": [
            {
                "self": "http://localhost:8090/jira/rest/api/2.0/status/10000",
                "description": "The issue is currently being worked on.",
                "iconUrl": "http://localhost:8090/jira/images/icons/progress.gif",
                "name": "In Progress",
                "id": "10000"
            },
            {
                "self": "http://localhost:8090/jira/rest/api/2.0/status/5",
                "description": "The issue is closed.",
                "iconUrl": "http://localhost:8090/jira/images/icons/closed.gif",
                "name": "Closed",
                "id": "5"
            }
        ]
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3031](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3031)

#### Getting versions of a project

To get the versions of a specific project, use getVersionsOfProject and specify the project key. This operation returns a JSON representation of the list of versions in the project.

**getVersionsOfProject**
```xml
<jira.getVersionsOfProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
</jira.getVersionsOfProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.

**Sample request**

Following is a sample request that can be handled by the getVersionsOfProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the getVersionsOfProject operation.

```json
[
    {
        "self": "http://localhost:8080/jira/rest/api/2/version/10000",
        "id": "10000",
        "description": "An excellent version",
        "name": "New Version 1",
        "archived": false,
        "released": true,
        "releaseDate": "2010-07-06",
        "overdue": true,
        "userReleaseDate": "6/Jul/2010",
        "projectId": 10000
    },
    {
        "self": "http://localhost:8080/jira/rest/api/2/version/10010",
        "id": "10010",
        "description": "Minor Bugfix version",
        "name": "Next Version",
        "archived": false,
        "released": false,
        "overdue": false,
        "projectId": 10000
    }
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3195](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3195)

#### Getting roles of a project

To get the roles of a specific project, use getRolesOfProject and specify the project key. This operation returns a JSON representation of the list of roles in the project, including each role's name and a link to more details.

**getRolesOfProject**
```xml
<jira.getRolesOfProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
</jira.getRolesOfProject>
```
**Properties**
* projectKey: The Identifier the project whose information you want to get.

**Sample request**

Following is a sample request that can be handled by the getRolesOfProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST"
}
```
**Sample response**

Given below is a sample response for the getRolesOfProject operation.

```json
{
    "Users": "http://localhost:8080/jira/rest/api/2/project/MKY/role/10001",
    "Administrators": "http://localhost:8080/jira/rest/api/2/project/MKY/role/10002",
    "Developers": "http://localhost:8080/jira/rest/api/2/project/MKY/role/10000"
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1710](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1710)

#### Getting information on a role

To get information about a specific role, use getRolesByIdOfProject and specify the project key and role ID. This operation returns a JSON representation of the role, including its name, ID, actors, and more.

**getRolesByIdOfProject**
```xml
<jira.getRolesByIdOfProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
    <roleId>{$ctx:roleId}</roleId>
</jira.getRolesByIdOfProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.
* roleId: Identifies the role whose information you want to get.

**Sample request**

Following is a sample request that can be handled by the getRolesByIdOfProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST",
    "roleId":"10360"
}
```
**Sample response**

Given below is a sample response for the getRolesByIdOfProject operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/project/MKY/role/10360",
    "name": "Developers",
    "id": 10360,
    "description": "A project role that represents developers in a project",
    "actors": [
        {
            "id": 10240,
            "displayName": "jira-developers",
            "type": "atlassian-group-role-actor",
            "name": "jira-developers"
        }
    ]
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1731](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1731)

#### Returns a list of users can be assigned issues for all the given projects

To get list of users that match the search string and can be assigned issues for all the given projects, use getUserAssignableProjects.

**getUserAssignableProjects**
```xml
<jira.getUserAssignableProjects>
    <projectKeys>{$ctx:projectKeys}</projectKeys>
    <usernameForSearch>{$ctx:usernameForSearch}</usernameForSearch>
    <maxResults>{$ctx:maxResults}</maxResults>
    <startAt>{$ctx:startAt}</startAt>
</jira.getUserAssignableProjects>
```
**Properties**
* projectKeys : The keys of the projects we are finding assignable users for, comma-separated.
* usernameForSearch : The username for search.
* maxResults : The maximum number of users to return.
* startAt : The index of the first user to return.

**Sample request**

Following is a sample request that can be handled by the getUserAssignableProjects operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectKeys":"TEST",
    "usernameForSearch":"fred"
}
```
**Sample response**

Given below is a sample response for the getUserAssignableProjects operation.

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
    ..
]
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3973](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e3973)

#### Assigning users to a role

To assign one or more users to a specific role in a project, use setActorsToRoleOfProject, specify the project key and role ID, and specify the users in the payload. You can specify individual users or groups.

**setActorsToRoleOfProject**
```xml
<jira.setActorsToRoleOfProject>
    <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
    <roleId>{$ctx:roleId}</roleId>
    <roles>{$ctx:roles}</roles>
</jira.setActorsToRoleOfProject>
```
**Properties**
* projectIdOrKey: The Identifier the project whose information you want to get.
* roleId: Identifies the role whose information you want to get.
* roles: The users who you want to assign.

**Sample request**

Following is a sample request that can be handled by the setActorsToRoleOfProject operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST",
    "projectKey":"JAF",
    "roleId":"10360",
    "roles":{"user" :["James"]}
}
```
**Sample response**

Given below is a sample response for the setActorsToRoleOfProject operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/project/MKY/role/10360",
    "name": "Developers",
    "id": 10360,
    "description": "A project role that represents developers in a project",
    "actors": [
        ...
    ]
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1731](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e1731)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the setActorsToRoleOfProject operation.
You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :
```xml
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="setActorsToRoleOfProject"
       transports="https,http"
       statistics="disable"
       trace="disable"
       startOnLoad="true">
   <target>
      <inSequence>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="projectIdOrKey" expression="json-eval($.projectIdOrKey)"/>
         <property name="roleId" expression="json-eval($.roleId)"/>
         <property name="roles" expression="json-eval($.roles)"/>
         <jira.init>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <uri>{$ctx:uri}</uri>
         </jira.init>
         <jira.setActorsToRoleOfProject>
            <projectIdOrKey>{$ctx:projectIdOrKey}</projectIdOrKey>
            <roleId>{$ctx:roleId}</roleId>
            <roles>{$ctx:roles}</roles>
         </jira.setActorsToRoleOfProject>
         <log level="full"/>
         <respond/>
      </inSequence>
      <outSequence/>
      <faultSequence/>
   </target>
   <description/>
</proxy>
```

2. Create a json file named setActorsToRoleOfProject.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "projectIdOrKey":"TEST",
    "projectKey":"JAF",
    "roleId":"10360",
    "roles":{"user" :["James"]}
}
```
3. Replace the credentials and details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/setActorsToRoleOfProject -H "Content-Type: application/json" -d @setActorsToRoleOfProject.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{
    "self": "http://localhost:8080/jira/rest/api/2/project/MKY/role/10360",
    "name": "Developers",
    "id": 10360,
    "description": "A project role that represents developers in a project",
    "actors": [
        ...
    ]
}
```
