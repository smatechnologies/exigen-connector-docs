# Installation
Installation consists of multiple steps that are required to complete the installation successfully. These steps consists of the folowing:
- Install a Windows Agent (if required).
- Install the Exigen Connector.
- Install the Exigen Windows job subtype. 
-  Configure the connector.

It should be noted that the Exigen Connector requires a Windows Agent as it executes as a Windows batch job. It can be installed either on the central server, the Exigen Application Server or an agent can be installed on another Windows server.

## Supported Software Levels
The following software levels are required to implement the Exigen Connector.
- Exigen BatchJobTrigger version 1.0.
- OpCon Release 19.x or higher.
- Uses embedded Java 1.8.

## Connector Installation

### Connector Installation
The Exigen Connector can be installed on the OpCon server or on a separate Windows server. When installing on a separate Windows server, it requires that an OpCon Windows Agent be installed on the server.

Copy the supplied install file ExigenConnector-win.zip file to the required windows system in a temp directory (c:\temp) and extract the files into the required location.

After the installation is complete, the installation root directory contains the connector executable, the Connector.config file, a java directory containing the required Java environment, a wsdl directory containing the BatchJobTrigger.wsdl file and an emplugins directory containing the Job Subtype.

### Job Subtype Installation
Copy the Enterprise Manager plug-in from the installation /emplugins directory to the dropins directory of the Enterprise Manager installation. If the dropins directory does not exist, create the dropins directory off the root directory. 

Restart Enterprise Manager and a new Windows job subtype called **Exigen**** will be visible when a Windows Job is selected.

If not restart Enterprise Manager using 'Run as Administrator'. After this Enterprise Manager can be used normally.

Create a global property **ExigenPath** that contains the full path of the installation directory.

### Connector Configuration
The configuration of the Exigen Connector requires setting the required values in the Connector.config file. The Connector.config file contains information that defines the address of the web services, the web services end point, the location of the BatchJobTrigger.wsdl file.

The Connector.config contains the following values

Property Name | Value
--------- | -----------
**[CONNECTOR]**                | header
**CONNECTOR_NAME**             | The name of the connector. This value should not change
**DEBUG**                      | The Connector supports a debug mode which can be enabled by setting the value to ON. The connector should be run with DEBUG disabled (OFF) and enabled (ON) when requested to capture an error condition. Value either ON or OFF (default OFF).
**[EXIGEN]**                   | header
**EXIGEN_SERVER_ADDRESS**      | This defines the address of the web server that supports the Exigen web services. The value here is used to overwrite the web server address in the supplied wsdl.
**EXIGEN_SERVICES_ENDPOINT**   | This defines the web services end point to be used when calling the web service.
**EXIGEN_WSDL_LOCATION**       | This defines the location of the BatchManage.wsdl file relative to the installation directory. This value should not be changed.

 
Example configuration file
```
[CONNECTOR]
CONNECTOR_NAME=Exigen Connector
DEBUG=OFF

[EXIGEN]
EXIGEN_SERVER_ADDRESS=http://localhost:8080
EXIGEN_SERVICE_ENDPOINT=/localhost/webservices/BatchJobTrigger
EXIGEN_WSDL_LOCATION=wsdl/BatchJobTrigger.wsdl

```
