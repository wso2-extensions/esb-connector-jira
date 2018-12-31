# Configuring JIRA Operations

[[Prerequisites]](#Prerequisites) [[Initializing the connector]](#initializing-the-connector)

## Prerequisites

> NOTE: To work with the JIRA connector, you need to have a JIRA account. If you do not have a JIRA account, [installing the JIRA software](https://confluence.atlassian.com/jirasoftwareserver/installing-jira-software-938845212.html) and create a JIRA account.

To use the JIRA connector, add the <jira.init> element in your configuration before carrying out any other JIRA operation.

This JIRA configuration authenticates with JIRA by specifying the user name, password, and URI of the JIRA instance.

### Enable Message Builder and Formatter

Ensure that the following Axis2 configurations are added and enabled in the <ESB_HOME>/repository/conf/axis2/axis2.xml file or in <EI_HOME>/conf/axis2/axis2.xml file.

* Required message formatter

    ```xml
        <messageFormatter contentType="multipart/form-data" class="org.wso2.carbon.relay.ExpandingMessageFormatter"/>
    ```
* Required message builder

    ```xml
        <messageBuilder contentType="multipart/form-data" class="org.wso2.carbon.relay.BinaryRelayBuilder"/>
    ```


> NOTE: If you want the connector to perform blocking invocations, you need to add and enable the following builders and formatter in the <ESB_HOME>/repository/conf/axis2/axis2_blocking_client.xml file or in <EI_HOME>/conf/axis2/axis2_blocking_client.xml file.

## Initializing the connector

Add the following <jira.init>  method in your configuration:
 
#### init
```xml
<jira.init>
    <username>{$ctx:username}</username>
    <password>{$ctx:password}</password>
    <uri>{$ctx:uri}</uri>
    <blocking>{$ctx:blocking}</blocking>
</jira.init>
```
**Properties** 
* username: The username of the user.
* password: The password of the user.
* uri: The instance URI of Jira account.
* blocking: Boolean type, this property helps the connector perform blocking invocations to Jira.

**Sample Request**

Following is a sample REST request that can be handled by the init operation.

```json
{
    "username":"admin",
    "password":"jira@jaffna",
    "uri":"http://localhost:8080",
    "blocking":"false"
}
```

**Related  documentation**

[https://developer.atlassian.com/server/jira/platform/basic-authentication/](https://developer.atlassian.com/server/jira/platform/basic-authentication/)

Now that you have connected to JIRA, use the information in the following topics to perform various operations with the connector. Also, see [Configuring the JIRA Connector Fault Handler Sequence]((fault_handler_sequence.md)).

[Working with Dashboards in JIRA](dashboards.md)

[Working with Filters in JIRA](filters.md)

[Working with Groups in JIRA](groups.md)

[Working with Issues in JIRA](issues.md)

[Working with Projects in JIRA](projects.md)

[Working with Search in JIRA](search.md)

[Working with Users in JIRA](users.md)

[Working with Attachments in JIRA](attachments.md)

[Working with Components in JIRA](components.md)

[Working with Issue Links in JIRA](links.md)