# Working with Search in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operation is available for working with search.Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with search, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [searchJira](#searching-for-issues)    | 	Search in JIRA using JQL. |

### Operation details

Following is more information about these operations.

#### Searching for issues
To get an existing issue, use searchJira and specify theJQL query.

**searchJira**
```xml
<jira.C>
    <query>{$ctx:query}</query>
    <maxResults>{$ctx:maxResults}</maxResults>
    <startAt>{$ctx:startAt}</startAt>
    <fields>{$ctx:fields}</fields>
    <validateQuery>{$ctx:validateQuery}</validateQuery>
    <expand>{$ctx:expand}</expand>
</jira.searchJira>
```
**Properties**
* query: The JQL expression to use for finding issues. The query must include an ORDER BY clause. For more information, see [Advanced Searching](https://confluence.atlassian.com/jiracoreserver073/advanced-searching-861257209.html) in the JIRA documentation.
* maxResults: Optional. The maximum number of issues to return, up to 1000 (default is 50).
* startAt : Optional. The 0-based index of the first issue to return (default is 0).
* fields : Specifies a comma-separated list of fields to be included in the response.
* validateQuery : Specify whether to validate the JQL query.
* expand : A comma-separated list of the parameters to expand.

**Sample request**

Following is a sample REST/JSON request that can be handled by the searchJira operation.
```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "query":"text~\"issue2\""
}
```
**Sample response**

Given below is a sample response for the searchJira operation.

```json
{
    "expand": "names,schema",
    "startAt": 0,
    "maxResults": 50,
    "total": 1,
    "issues": [
        {
            "expand": "",
            "id": "10001",
            "self": "http://localhost:8080/jira/rest/api/2/issue/10001",
            "key": "HSP-1"
        }
    ]
}
```

**Related JIRA documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4074](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e4074)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the searchJira operation. You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :
```xml
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="searchJira"
       transports="https http"
       startOnLoad="true"
       trace="disable">
   <description/>
   <target>
      <inSequence>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="query" expression="json-eval($.query)"/>
         <property name="maxResults" expression="json-eval($.maxResults)"/>
         <property name="startAt" expression="json-eval($.startAt)"/>
         <property name="fields" expression="json-eval($.fields)"/>
         <property name="validateQuery" expression="json-eval($.validateQuery)"/>
         <property name="expand" expression="json-eval($.expand)"/>
         <jira.init>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <uri>{$ctx:uri}</uri>
         </jira.init>
         <jira.searchJira>
            <query>{$ctx:query}</query>
            <maxResults>{$ctx:maxResults}</maxResults>
            <startAt>{$ctx:startAt}</startAt>
            <fields>{$ctx:fields}</fields>
            <validateQuery>{$ctx:validateQuery}</validateQuery>
            <expand>{$ctx:expand}</expand>
         </jira.searchJira>
         <log level="full"/>
         <respond/>
      </inSequence>
      <outSequence/>
      <faultSequence/>
   </target>
</proxy>
```

2. Create a json file named searchJira.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "query":"text~\"issue2\""
}
```
3. Replace the credentials and details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/searchJira -H "Content-Type: application/json" -d @searchJira.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{
    "expand": "names,schema",
    "startAt": 0,
    "maxResults": 50,
    "total": 1,
    "issues": [
        {
            "expand": "",
            "id": "10001",
            "self": "http://localhost:8080jira/rest/api/2/issue/10001",
            "key": "HSP-1"
        }
    ]
}
```
