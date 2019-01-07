# Working with Dashboards in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operations allow you to work with dashboards, Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with dashboards, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [getDashboards](#getting-dashboards)    | Gets all available JIRA dashboards. |
| [getDashboardById](#getting-a-specific-dashboard)      | Gets a specific dashboard. |
### Operation details

This section provides more details on each of the operations.

#### Getting dashboards
This operation returns a JSON representation of the list of dashboards, including their names, IDs, and more.
**getDashboards**
```xml
<jira.getDashboards>
    <maxResults>{$ctx:maxResults}</maxResults>
    <filter>{$ctx:filter}</filter>
    <startAt>{$ctx:startAt}</startAt>
</jira.getDashboards>
```

**Properties**
* maxResults: The maximum number of users to return, up to 1000 (default is 50).
* startAt : The index of the first dashboard to return (0-based). must be 0 or a multiple of maxResults.
* filter : An optional filter that is applied to the list of dashboards.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getDashboards operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "maxResults":"50",
    "filter":"favourite"
}
```
**Sample response**

Given below is a sample response for the getDashboards operation.

```json
{
    "startAt": 0,
    "maxResults": 50,
    "total": 1,
    "dashboards": [
        {
            "id": "10100",
            "name": "test",
            "self": "http://localhost:8080/rest/api/2/dashboard/10100",
            "view": "http://localhost:8080/secure/Dashboard.jspa?selectPageId=10100"
        }
    ]
}
```

**Related Jira Documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e816](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e816)

#### Getting a specific dashboard

This operation returns a JSON representation of the dashboard details, including its name, ID, and more.

**getDashboardById**
```xml
<jira.getDashboardById>
  <id>{$ctx:id}</id>
</jira.getDashboardById>
```

**Properties**
* id: Identifies the dashboard whose details you want to get.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getDashboardById operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "id":"10100"
}
```
**Sample response**

Given below is a sample response for the getDashboardById operation.

```json
{
    "id": "10100",
    "name": "test",
    "self": "http://localhost:8080/rest/api/2/dashboard/10100",
    "view": "http://localhost:8080/secure/Dashboard.jspa?selectPageId=10100"
}
```

**Related Jira documentation**

[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e843](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e843)

### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the getDashboardById operation. You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :

```xml
<proxy xmlns="http://ws.apache.org/ns/synapse"
       name="getDashboardById"
       transports="https http"
       startOnLoad="true"
       trace="disable">
   <description/>
   <target>
      <inSequence>
         <property name="username" expression="json-eval($.username)"/>
         <property name="password" expression="json-eval($.password)"/>
         <property name="uri" expression="json-eval($.uri)"/>
         <property name="id" expression="json-eval($.id)"/>
         <jira.init>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
            <uri>{$ctx:uri}</uri>
         </jira.init>
         <jira.getDashboardById>
            <id>{$ctx:id}</id>
         </jira.getDashboardById>
         <log level="full"/>
         <respond/>
      </inSequence>
      <outSequence/>
      <faultSequence/>
   </target>
</proxy>
```

2. Create a json file named getDashboardById.json and copy the configurations given below to it:

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "id":"10100"
}
```
3. Replace the credentials and details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/getDashboardById -H "Content-Type: application/json" -d @getDashboardById.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{
    "id": "10100",
    "name": "test",
    "self": "http://localhost:8080/rest/api/2/dashboard/10100",
    "view": "http://localhost:8080/secure/Dashboard.jspa?selectPageId=10100"
}
```
