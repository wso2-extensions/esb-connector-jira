# Working with Filters in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operations are available for working with filters.Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with filters, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [getFilterById](#getting-a-filter)    |  	Gets the specified filter. |
| [getFavoriteFilters](#getting-favorite-filters)    |  	Gets the favorite filters of the current user. |
| [createFilter](#creating-a-filter)    |  	Creates a new filter. |
| [updateFilterById](#updating-a-filter)    |  	Updates a filter. |
| [deleteFilter](#delete-a-filter)    |  	Deletes a filter. |

### Operation details

This section provides further details on the operation related to filters.

#### Getting a filter
To get information about a specific filter, use getFilterById and specify the filter ID. This operation returns a JSON representation of the filter information, including the name, ID, search URL, and more.

**getFilterById**
```xml
<jira.getFilterById>
    <filterId>{$ctx:filterId}</filterId>
    <expand>{$ctx:expand}</expand>
</jira.getFilterById>
```

**Properties**
* filterId : Identifies the filter whose information you want to get.
* expand : The parameters to expand.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getFilterById operation.
```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "filterId":"10100"
}
```
**Sample response**

Given below is a sample response for the getFilterById operation.

```json
{
    "self": "http://localhost:8080/rest/api/2/filter/10100",
    "id": "10100",
    "name": "All Open Bugs",
    "description": "Lists all open bugs",
    "owner": {
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
    "jql": "type = Bug AND resolution is EMPTY",
    "viewUrl": "http://localhost:8080/issues/?filter=10100",
    "searchUrl": "http://localhost:8080/rest/api/2/search?jql=type+%3D+Bug+AND+resolution+is+EMPTY",
    "favourite": true,
    "sharePermissions": [],
    "editable": true,
    "sharedUsers": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    },
    "subscriptions": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    }
}
```

**Related JIRA API**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4252](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4252)

#### Getting favorite filters
To get the favorite filters of the current user, use getFavouriteFilter. This operation returns a JSON representation of the filters, including their names, IDs, search URLs, and more.
**getFavouriteFilters**
```xml
<jira.getFavouriteFilters>
    <expand>{$ctx:expand}</expand>
</jira.getFavouriteFilters>
```

**Properties**
* expand : The parameters to expand.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getFavouriteFilters operation.
```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080"
}
```
**Sample response**

Given below is a sample response for the getFavouriteFilters operation.

```json
[
    {
        "self": "http://localhost:8080/rest/api/2/filter/10100",
        "id": "10100",
        "name": "All Open Bugs",
        "description": "Lists all open bugs",
        "owner": {
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
        "jql": "type = Bug AND resolution is EMPTY",
        "viewUrl": "http://localhost:8080/issues/?filter=10100",
        "searchUrl": "http://localhost:8080/rest/api/2/search?jql=type+%3D+Bug+AND+resolution+is+EMPTY",
        "favourite": true,
        "sharePermissions": [],
        "editable": true,
        "sharedUsers": {
            "size": 0,
            "items": [],
            "max-results": 1000,
            "start-index": 0,
            "end-index": 0
        },
        "subscriptions": {
            "size": 0,
            "items": [],
            "max-results": 1000,
            "start-index": 0,
            "end-index": 0
        }
    }
]
```

**Related JIRA API**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4319](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4319)

#### Creating a filter
To create a new filter, use createFilter and attach the JSON representation of the filter as the payload of the request.

**createFilter**
```xml
<jira.createFilter>
    <filterName>{$ctx:filterName}</filterName>
    <description>{$ctx:description}</description>
    <jqlType>{$ctx:jqlType}</jqlType>
    <favourite>{$ctx:favourite}</favourite>
</jira.createFilter>
```

**Properties**
* filterName : The name of the filter.
* description : The description of the filter.
* jqlType : The jqlType of the filter.
* favourite : Specify whether favourite.

**Sample request**

Following is a sample REST/JSON request that can be handled by the createFilter operation.
```json
{
   "username":"admin",
   "password":"jira@jaffna",
   "uri":"http://localhost:8080",
   "filterName":"All Open Bugs",
   "description":"Lists all open bugs",
   "jqlType":"Bug and resolution is empty",
   "favourite":"true"
}
```
**Sample response**

Given below is a sample response for the createFilter operation.

```json
{
    "self": "http://localhost:8080/rest/api/2/filter/10100",
    "id": "10100",
    "name": "All Open Bugs",
    "description": "Lists all open bugs",
    "owner": {
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
    "jql": "type = Bug AND resolution is EMPTY",
    "viewUrl": "http://localhost:8080/issues/?filter=10100",
    "searchUrl": "http://localhost:8080/rest/api/2/search?jql=type+%3D+Bug+AND+resolution+is+EMPTY",
    "favourite": true,
    "sharePermissions": [],
    "editable": true,
    "sharedUsers": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    },
    "subscriptions": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    }
}
```

**Related JIRA API**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4220](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4220)

#### Updating a filter
To update an existing filter, use updateFilterById,  specify the filter ID.

**updateFilterById**
```xml
<jira.updateFilterById>
    <filterId>{$ctx:filterId}</filterId>
    <filterName>{$ctx:filterName}</filterName>
    <description>{$ctx:description}</description>
    <jqlType>{$ctx:jqlType}</jqlType>
    <favourite>{$ctx:favourite}</favourite>
</jira.updateFilterById>
```

**Properties**
* filterId : The id of the filter.
* filterName : The name of the filter.
* description : The description of the filter.
* jqlType : The jqlType of the filter.
* favourite : Specify whether favourite.
* expand : The parameters to expand.

**Sample request**
Following is a sample REST/JSON request that can be handled by the updateFilterById operation.

```json
{
   "username":"admin",
   "password":"jira@jaffna",
   "uri":"http://localhost:8080",
   "filterName":"All  Bugs",
   "description":"Lists all bugs",
   "jqlType":"Bug and resolution is empty",
   "favourite":"true",
   "filterId":"10101"
}
```
**Sample response**

Given below is a sample response for the updateFilterById operation.

```json
{
    "self": "http://localhost:8080/rest/api/2/filter/10101",
    "id": "10101",
    "name": "All  Bugs",
    "description": "Lists all bugs",
    "owner": {
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
    "jql": "type = Bug AND resolution is EMPTY",
    "viewUrl": "http://localhost:8080/issues/?filter=10101",
    "searchUrl": "http://localhost:8080/rest/api/2/search?jql=type+%3D+Bug+AND+resolution+is+EMPTY",
    "favourite": true,
    "sharePermissions": [],
    "editable": true,
    "sharedUsers": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    },
    "subscriptions": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    }
}
```

**Related JIRA API**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4277](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4277)

#### Delete a filter
To delete a filter, use deleteFilter and specify the filter ID.
**deleteFilter**
```xml
<jira.deleteFilter>
    <filterId>{$ctx:filterId}</filterId>
</jira.deleteFilter>
```

**Properties**
* filterId: Identifies the filter whose information you want to get.

**Sample request**
Following is a sample REST/JSON request that can be handled by the deleteFilter operation.

```json
{
   "username":"admin",
   "password":"jira@jaffna",
   "uri":"https://testcon.atlassian.net",
   "filterId":"10101"
}
```
**Sample response**

For the successful response, you will get 204 No Content status code without any body.

**Related JIRA API**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4306](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4306)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the createFilter operation. You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :

```xml
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="createFilter"
       transports="https http"
       startOnLoad="true"
       trace="disable">
   <description/>
   <target>
      <inSequence>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="filterName" expression="json-eval($.filterName)"/>
         <property name="description" expression="json-eval($.description)"/>
         <property name="jqlType" expression="json-eval($.jqlType)"/>
         <property name="favourite" expression="json-eval($.favourite)"/>
         <jira.init>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <uri>{$ctx:uri}</uri>
         </jira.init>
         <jira.createFilter>
            <filterName>{$ctx:filterName}</filterName>
            <description>{$ctx:description}</description>
            <jqlType>{$ctx:jqlType}</jqlType>
            <favourite>{$ctx:favourite}</favourite>
         </jira.createFilter>
         <log level="full"/>
         <respond/>
      </inSequence>
      <outSequence/>
      <faultSequence/>
   </target>
</proxy>
```

2. Create a json file named createFilter.json and copy the configurations given below to it:

```json
{
   "username":"admin",
   "password":"jira@jaffna",
   "uri":"http://localhost:8080",
   "filterName":"All Open Bugs",
   "description":"Lists all open bugs",
   "jqlType":"Bug and resolution is empty",
   "favourite":"true"
}
```
3. Replace the credentials with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/createFilter -H "Content-Type: application/json" -d @createFilter.json
```

5. Jira returns a json response similar to the one shown below:
 
```json
{
    "self": "http://localhost:8080/rest/api/2/filter/10100",
    "id": "10100",
    "name": "All Open Bugs",
    "description": "Lists all open bugs",
    "owner": {
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
    "jql": "type = Bug AND resolution is EMPTY",
    "viewUrl": "http://localhost:8080/issues/?filter=10100",
    "searchUrl": "http://localhost:8080/rest/api/2/search?jql=type+%3D+Bug+AND+resolution+is+EMPTY",
    "favourite": true,
    "sharePermissions": [],
    "editable": true,
    "sharedUsers": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    },
    "subscriptions": {
        "size": 0,
        "items": [],
        "max-results": 1000,
        "start-index": 0,
        "end-index": 0
    }
}
```
