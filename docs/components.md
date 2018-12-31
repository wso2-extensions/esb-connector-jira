# Working with Components in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operations allow you to work with components. Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with components, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [createComponent](#creating-a-component)    | Creates a component. |
| [getComponent](#retrieving-a-project-component)      | Retrieves a project component. |
| [updateComponent](#modifying-a-component)      | Modifies a component. |
| [countComponentRelatedIssues](#retrieving-counts-of-issues )      | Retrieves counts of issues related to this component. |

### Operation details

This section provides further details on the operations related to components.

#### creating a component
The createComponent operation creates a component.

**createComponent**
```xml
<jira.createComponent>
    <name>{$ctx:name}</name>
    <project>{$ctx:project}</project>
    <description>{$ctx:description}</description>
    <leadUserName>{$ctx:leadUserName}</leadUserName>
    <assigneeType>{$ctx:assigneeType}</assigneeType>
    <isAssigneeTypeValid>{$ctx:isAssigneeTypeValid}</isAssigneeTypeValid>
</jira.createComponent>
```

**Properties**

* name: The name of the component.
* project: The key of the project, the component should be belong to.
* description: The description for the component.
* leadUserName: The key of the lead user name.
* assigneeType: The type of the assignee.
* isAssigneeTypeValid: A Boolean which specifies whether the assignee type is valid or not.

**Sample request**

Following is a sample REST/JSON request that can be handled by the createComponent operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "name": "testing component1",
    "project": "TESTPM1",
    "description": "test description",
    "leadUserName": "admin",
    "assigneeType": "PROJECT_LEAD",
    "isAssigneeTypeValid": "false"
}
```
**Sample response**

Given below is a sample response for the createComponent operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/component/10000",
    "id": "10000",
    "name": "Component 1",
    "description": "This is a JIRA component",
    "lead": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "avatarUrls": {
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
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
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
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
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
            "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
        },
        "displayName": "Fred F. User",
        "active": false
    },
    "isAssigneeTypeValid": false
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/5.0.html#id197647](https://developer.atlassian.com/static/rest/jira/5.0.html#id197647)

#### Retrieving a project component

The getComponent operation retrieves a project component.
**getComponent**
```xml
<jira.getComponent>
    <componentId>{$ctx:componentId}</componentId>
</jira.getComponent>
```
**Properties**
* componentId: The unique identifier for a particular component.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getComponent operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "componentId": "10000"
}
```
**Sample response**

Given below is a sample response for the getComponent operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/component/10000",
    "id": "10000",
    "name": "Component 1",
    "description": "This is a JIRA component",
    "lead": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "avatarUrls": {
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
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
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
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
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
            "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
        },
        "displayName": "Fred F. User",
        "active": false
    },
    "isAssigneeTypeValid": false
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/5.0.html#id197800](https://developer.atlassian.com/static/rest/jira/5.0.html#id197800)

#### Modifying a component

The updateComponent operation modifies a component.

**updateComponent**
```xml
<jira.updateComponent>
    <componentId>{$ctx:componentId}</componentId>
    <name>{$ctx:name}</name>
    <description>{$ctx:description}</description>
    <leadUserName>{$ctx:leadUserName}</leadUserName>
    <assigneeType>{$ctx:assigneeType}</assigneeType>
    <isAssigneeTypeValid>{$ctx:isAssigneeTypeValid}</isAssigneeTypeValid>
</jira.updateComponent>
```
**Properties**

* componentId: The unique identifier for a particular component.
* name: The name of the component.
* description: The description for the component.
* leadUserName: The key of the lead username.
* assigneeType: The type of the assignee.
* isAssigneeTypeValid: A Boolean which specifies whether the assignee type is valid or not.

**Sample request**

Following is a sample REST/JSON request that can be handled by the updateComponent operation.
```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "componentId": "10000",
    "name": "testing component1",
    "description": "test description",
    "leadUserName": "admin",
    "assigneeType": "PROJECT_LEAD",
    "isAssigneeTypeValid": "false"
}
```
**Sample response**

Given below is a sample response for the updateComponent operation.

```json
{
    "self": "http://localhost:8080/rest/api/2/component/10000",
    "id": "10000",
    "name": "testing component1",
    "description": "test description",
    "lead": {
        "self": "http://localhost:8080/rest/api/2/user?username=admin",
        "key": "admin",
        "name": "admin",
        "avatarUrls": {
            "48x48": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=48",
            "24x24": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=24",
            "16x16": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=16",
            "32x32": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=32"
        },
        "displayName": "admin@gmail.com",
        "active": true
    },
    "assigneeType": "PROJECT_LEAD",
    "assignee": {
        "self": "http://localhost:8080/rest/api/2/user?username=admin",
        "key": "admin",
        "name": "admin",
        "avatarUrls": {
            "48x48": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=48",
            "24x24": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=24",
            "16x16": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=16",
            "32x32": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=32"
        },
        "displayName": "admin@gmail.com",
        "active": true
    },
    "realAssigneeType": "PROJECT_LEAD",
    "realAssignee": {
        "self": "http://localhost:8080/rest/api/2/user?username=admin",
        "key": "admin",
        "name": "admin",
        "avatarUrls": {
            "48x48": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=48",
            "24x24": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=24",
            "16x16": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=16",
            "32x32": "https://www.gravatar.com/avatar/9f2ee74106e4d9afc58bb796a0895908?d=mm&s=32"
        },
        "displayName": "admin@gmail.com",
        "active": true
    },
    "isAssigneeTypeValid": true,
    "project": "KANA",
    "projectId": 10000
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/5.0.html#id197853](https://developer.atlassian.com/static/rest/jira/5.0.html#id197853)

#### Retrieving counts of issues

The countComponentRelatedIssues operation retrieves counts of issues related to this component.

**countComponentRelatedIssues**
```xml
<jira.countComponentRelatedIssues>
    <componentId>{$ctx:componentId}</componentId>
</jira.countComponentRelatedIssues>
```
**Properties**
* componentId: The unique identifier for a particular component.

**Sample request**

Following is a sample REST/JSON request that can be handled by the countComponentRelatedIssues operation.

```json
{
    "uri": "http://localhost:8080",
    "username": "admin",
    "password": "1qaz2wsx@",
    "componentId": "10000"
}
```
**Sample response**

Given below is a sample response for the searchIssueViewableUsers operation.

```json
{
    "self": "http://localhost:8080/jira/rest/api/2/component/10000",
    "issueCount": 23
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/5.0.html#id197913](https://developer.atlassian.com/static/rest/jira/5.0.html#id197913)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to JIRA with the init operation and use the createComponent operation.  You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxy name="jira_createComponent" startOnLoad="true" statistics="disable" trace="disable" transports="https" xmlns="http://ws.apache.org/ns/synapse">
   <target>
      <inSequence onError="faultHandlerSeq">
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="name" expression="json-eval($.name)"/>
         <property name="project" expression="json-eval($.project)"/>
         <property name="description" expression="json-eval($.description)"/>
         <property name="leadUserName" expression="json-eval($.leadUserName)"/>
         <property name="assigneeType" expression="json-eval($.assigneeType)"/>
         <property name="isAssigneeTypeValid" expression="json-eval($.isAssigneeTypeValid)"/>
         <jira.init>
            <uri>{$ctx:uri}</uri>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
         </jira.init>
         <jira.createComponent>
            <name>{$ctx:name}</name>
            <project>{$ctx:project}</project>
            <description>{$ctx:description}</description>
            <leadUserName>{$ctx:leadUserName}</leadUserName>
            <assigneeType>{$ctx:assigneeType}</assigneeType>
            <isAssigneeTypeValid>{$ctx:isAssigneeTypeValid}</isAssigneeTypeValid>
         </jira.createComponent>
         <respond/>
      </inSequence>
      <outSequence>
         <send/>
      </outSequence>
   </target>
   <description/>
</proxy>
```

2. Create a json file named jira_createComponent.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "usernameFilter":"admin"
}
```
3. Replace the credentials and the details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/jira_createComponent -H "Content-Type: application/json" -d @jira_createComponent.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{
    "self": "http://localhost:8080/jira/rest/api/2/component/10000",
    "id": "10000",
    "name": "Component 1",
    "description": "This is a JIRA component",
    "lead": {
        "self": "http://localhost:8080/jira/rest/api/2/user?username=fred",
        "name": "fred",
        "avatarUrls": {
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
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
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
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
            "16x16": "http://localhost:8080/jira/secure/useravatar?size=small&ownerId=fred",
            "48x48": "http://localhost:8080/jira/secure/useravatar?size=large&ownerId=fred"
        },
        "displayName": "Fred F. User",
        "active": false
    },
    "isAssigneeTypeValid": false
}
```
