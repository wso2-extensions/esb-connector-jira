### JIRA ESB/EI Connector

The JIRA [Connector](https://docs.wso2.com/display/EI650/Working+with+Connectors) allows you to connect to JIRA, an online issue-tracking database. The connector uses the JIRA REST API to connect to JIRA, view and update issues, work with filters, and more.

## Compatibility

| Connector version | Supported JIRA REST API version | Supported WSO2 ESB/EI version |
| ------------- | ------------- | ------------- |
| [1.0.5](https://github.com/wso2-extensions/esb-connector-jira/tree/org.wso2.carbon.connector.jira-1.0.5) | v2.0 | EI 6.5.0 |
| [1.0.4](https://github.com/wso2-extensions/esb-connector-jira/tree/org.wso2.carbon.connector.jira-1.0.4) | v2.0 | ESB 4.9.0, 5.0.0, EI 6.1.0, 6.1.1, 6.2.0, 6.3.0, 6.4.0 |
| [1.0.3](https://github.com/wso2-extensions/esb-connector-jira/tree/org.wso2.carbon.connector.jira-1.0.3) | v2.0 | ESB 4.9.0, 5.0.0, EI 6.1.0, 6.1.1, 6.2.0, 6.3.0, 6.4.0 |
| [1.0.2](https://github.com/wso2-extensions/esb-connector-jira/tree/org.wso2.carbon.connector.jira-1.0.2) | v2.0 | ESB 4.9.0, 5.0.0 |
| [1.0.1](https://github.com/wso2-extensions/esb-connector-jira/tree/org.wso2.carbon.connector.jira-1.0.1) | v2.0 | ESB 4.9.0 |
| [1.0.0](https://github.com/wso2-extensions/esb-connector-jira/tree/org.wso2.carbon.connector.jira-1.0.0) | v2.0 | ESB 4.9.0 |

## Getting started

#### Download and install the connector

1. Download the connector from the [WSO2 Store](https://store.wso2.com/store/assets/esbconnector/details/df59ac1e-88e7-46af-9b0a-f0f5f1e1b456) by clicking the Download Connector button.
2. Then, you can follow this [documentation](https://docs.wso2.com/display/EI650/Working+with+Connectors+via+Tooling) to add and enable the connector in your EI instance.
3. For more information on using connectors and their operations in your EI configurations, see [Using a Connector](https://docs.wso2.com/display/EI650/Using+a+Connector).

#### Configuring the connector operations

To get started with JIRA REST connector and their operations, see [Configuring JIRA Operations](docs/config.md).


## Building From the Source

Follow the steps given below to build the JIRA REST connector from the source code:

1. Get a clone or download the source from [Github](https://github.com/wso2-extensions/esb-connector-jira).
2. Run the following Maven command from the `esb-connector-jira` directory: `mvn clean install`.
3. The JIRA connector zip file is created in the `esb-connector-jira/target` directory

## How You Can Contribute

As an open source project, WSO2 extensions welcome contributions from the community.
Check the [issue tracker](https://github.com/wso2-extensions/esb-connector-jira/issues) for open issues that interest you. We look forward to receiving your contributions.
