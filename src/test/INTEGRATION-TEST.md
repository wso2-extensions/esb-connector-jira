## Integration tests for WSO2 ESB Jira connector

### Pre-requisites:

 - Maven 3.x
 - Java 1.8

Tested Platform: 

 - Mac OS 10.12.6
 - WSO2 EI 6.4.0
 - Java 1.8

Steps to follow in setting integration test.

 1. Download EI 6.4.0 from the official website

 2. To work with the JIRA connector, you need to have a JIRA account. If you do not have a JIRA account,
  [installing the JIRA software](https://confluence.atlassian.com/jirasoftwareserver/installing-jira-software-938845212.html)
  and create a JIRA account and keep the username,password and the URI for further reference.

 3. Create a project. Keep the project key for further reference.

 4. Create two users by navigating to Administration -> User management and keep the usernames for the further reference. (E.g user1 , user2)
 Keep one of the user as an optional user (E.g user1) for the account and verify it, keep the username, password for further reference.

 5. Create two issues (E.g issue1, issue2) under the project created in step 3. Add one of the users (E.g user2) created in step 4 (who is not verified with the account),
  as a watcher to one of the issues created (say issue1). Keep the issue keys and watcher username for further reference. Add an attachment to other issue (say issue2) and keep the issue id for further reference.

 6. Before you start performing various operations with the connector, make sure to place the Jira certificate to the location
       "<JIRA_CONNECTOR_HOME>/repository/.

 7. Navigate to location "<EI_HOME>/repository/conf/axis2" and add/uncomment following lines in "axis2.xml".

    	   Message Formatters :
               <messageFormatter contentType="text/html" class="org.wso2.carbon.relay.ExpandingMessageFormatter"/>

           Message Builders :
               <messageBuilder contentType="text/html" class="org.wso2.carbon.relay.BinaryRelayBuilder"/>

8. Compress modified EI as wso2ei-6.4.0.zip and copy that zip file in to location "{JIRA_HOME}/repository".

9. Update the esb-connector-jira properties file at location "<JIRA_CONNECTOR_HOME>/repository/ with the suited values.

10. Following are the properties used in the 'esb-connector-jira.properties' file and jira properties file at
location "JIRA_HOME}/src/test/resources/artifacts/ESB/connector/config" to run the integration tests.
```
    i)     apiUrl                      - Use the API URL as http://localhost:8080
   ii)     username                    - Use the username obtained in step 2.
  iii)     password                    - Use the password obtained in step 2.
   iv)     project                     - Use the key of the project obtained in step 3.
    v)     optionalUsername            - Use the username obtained in step 4 who is verified with the account (Eg user1).
   vi)     optionalPassword            - Use the password obtained in step 4 who is verified with the account.
  vii)     leadUserName                - Use the other username of a user created in step 4 who is not verified with the account (E.g user2).
 viii)     issueIdWithWatchList        - Use the key of the issue which has a watcher created in step 5 (E.g issue1).
   iX)     issueIdOrKey                - Use the other issue key which has a attachment on it. (E.g issue2)
    x)     componentNameMandatory      - Use a string value as the name of the component.
   xi)     componentNameOptional       - Use a string value as the name of the component.
  xii)     assigneeType                - Use 'PROJECT_LEAD' as the value.
 xiii)     componentDescription        - Use a string value as the description of the component.
  xiv)     updatedComponentName        - Use a string value as the name of the component.
   xv)     updatedComponentDescription - Use a string value as the description of the component.
  xvi)     updatedAssigneeType         - Use 'PROJECT_DEFAULT' as the value.
  xvii)    summary                     - Use a string value as the summary.
 xviii)    label                       - Use a string value as the label.
  xix)     description                 - Use a string value as the description.
   xx)     summaryOptional             - Use a string value as the summary.
   xxi)    expand                      - Use a valid string value for expand. e.g.:renderedBody
  xxii)    notificationSubject         - Use a string value as the notification subject.
 xxiii)    issueLinkType               - Use a valid string value for issue link type. e.g.: Duplicate
   ```

 > NOTE : Before running the integration test each time make sure the following:
  ```
   1. To make the "testRemoveUserFromWatcherListWithMandatoryParameters" pass, you have to add the same user name (say user2)
      as a watcher again to the same issue (issue1) before you remove the watcher from the issue.
   2. To make the "testAddVotesForIssueWithMandatoryParameters" pass, make sure the same user name (optionlal username) already added the vote to the issue or not. If the same user can't add vote again and again.
   ```

 8. Navigate to "<JIRA_HOME>/" and run the following command. </br>
 
    `$ mvn clean install -Dskip-tests=false`
