# Working with Attachments in JIRA

[[Overview]](#overview)  [[Operation details]](#operation-details)  [[Sample configuration]](#sample-configuration)

### Overview 

The following operation is available when working with attachments. Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with attachments, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [getAttachmentById](#retrieving-the-meta-data-for-an-attachmen)    | 	Retrieves the meta-data for an attachment, including the URL of the actual attached file. |
| [getAttachmentContent](#retrieving-the-content-for-an-attachment)      | 	Returns the content of an attachment.|

### Operation details

Following is more information about these operations.
#### Retrieving the meta-data for an attachment

This operation retrieves the meta-data for an attachment, including the URL of the actual attached file.

**getAttachmentById**
```xml
<jira.getAttachmentById>
    <attachmentId>{$ctx:attachmentId}</attachmentId>
</jira.getAttachmentById
```
**Properties**
* attachmentId: The ID to view the meta data of the attachment.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getAttachmentById operation.
```json
{
  "uri": "http://localhost:8080",
  "username": "admin",
  "password": "1qaz2wsx@",
  "attachmentId": "10000"
}
```
**Sample response**

Given below is a sample response for the getAttachmentById operation.

```json
{
    "self": "http://localhost:8080/rest/api/2/attachment/10000",
    "filename": "31714367_1982813478396639_3541297709187072000_n.jpg",
    "author": {
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
    "created": "2018-12-09T22:59:08.690+0530",
    "size": 45364,
    "mimeType": "image/jpeg",
    "properties": {},
    "content": "http://localhost:8080/secure/attachment/10000/31714367_1982813478396639_3541297709187072000_n.jpg",
    "thumbnail": "http://localhost:8080/secure/thumbnail/10000/_thumb_10000.png"
}
```

**Related Jira documentation**
[https://developer.atlassian.com/static/rest/jira/6.1.html#d2e168](https://developer.atlassian.com/static/rest/jira/6.1.html#d2e168)

#### Retrieving the content for an attachment

This operation retrieves the content of an attachment.
**getAttachmentContent**
```xml
<jira.getAttachmentContent>
    <attachmentUrl>{$ctx:attachmentUrl}</attachmentUrl>
    <fileType>{$ctx:fileType}</fileType>
</jira.getAttachmentContent>
```
**Properties**
* attachmentUrl: The URI of the attached file.
* fileType: Type of the attachment.

**Sample request**

Following is a sample REST/JSON request that can be handled by the getAttachmentContent operation.
```json
{
  "uri": "http://localhost:8080",
  "username": "admin",
  "password": "1qaz2wsx@",
  "attachmentUrl": "http://localhost:8080/secure/attachment/10000/31714367_1982813478396639_3541297709187072000_n.jpg",
  "fileType":"image/jpg"
}
```
**Sample response**

You will get 200 response code with the attached image as a response.


### Sample configuration

Following is a sample proxy service that illustrates how to connect to Jira with the init operation and use the getAttachmentById operation. You can use this sample as a template for using other operations in this category.

1. Create a sample proxy as below :
```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxy xmlns="http://ws.apache.org/ns/synapse" name="jira_getAttachmentById" transports="https" statistics="disable"
   trace="disable" startOnLoad="true">
   <target>
      <inSequence>
         <property name="uri" expression="json-eval($.uri)" />
         <property name="username" expression="json-eval($.username)" />
         <property name="password" expression="json-eval($.password)" />
         <property name="attachmentId" expression="json-eval($.attachmentId)" />
         <jira.init>
            <uri>{$ctx:uri}</uri>
            <username>{$ctx:username}</username>
            <password>{$ctx:password}</password>
         </jira.init>
         <jira.getAttachmentById>
            <attachmentId>{$ctx:attachmentId}</attachmentId>
         </jira.getAttachmentById>
         <respond />
      </inSequence>
      <outSequence>
         <send />
      </outSequence>
   </target>
   <description />
</proxy>
```

2. Create a json file named jira_getAttachmentById.json and copy the configurations given below to it:

```json
{
  "uri": "http://localhost:8080",
  "username": "admin",
  "password": "1qaz2wsx@",
  "attachmentId": "10000"
}
```
3. Replace the credentials and details with your values.

4. Execute the following curl command:

```bash
curl http://localhost:8280/services/jira_getAttachmentById -H "Content-Type: application/json" -d @jira_getAttachmentById.json
```
5. Jira returns a json response similar to the one shown below:
 
```json
{{
     "self": "http://localhost:8080/rest/api/2/attachment/10000",
     "filename": "31714367_1982813478396639_3541297709187072000_n.jpg",
     "author": {
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
     "created": "2018-12-09T22:59:08.690+0530",
     "size": 45364,
     "mimeType": "image/jpeg",
     "properties": {},
     "content": "http://localhost:8080/secure/attachment/10000/31714367_1982813478396639_3541297709187072000_n.jpg",
     "thumbnail": "http://localhost:8080/secure/thumbnail/10000/_thumb_10000.png"
 }