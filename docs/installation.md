---
title: Installation
sidebar_label: Installation
description: "Install the Exigen Connector, configure it to connect to the Exigen web service, and add the job subtype to Enterprise Manager."
tags:
  - Procedural
  - System Administrator
  - Installation
---

# Installation

## What is it?

The Exigen Connector installation places the connector software on a Windows server where an OpCon Windows Agent is installed. Installation also includes deploying the Exigen job subtype to Enterprise Manager and configuring the connector to communicate with the Exigen web service.

- Use this procedure when setting up the Exigen Connector for the first time
- Use this procedure when moving the connector to a new server
- Complete this procedure before creating any Exigen jobs in OpCon

## Prerequisites

Before installing the Exigen Connector, verify the following:

- An OpCon Windows Agent is installed on the target server (or on the OpCon server if installing there)
- The Exigen BatchJobTrigger web service (version 1.0) is accessible from the installation server
- Enterprise Manager is installed and running on the workstation where you will deploy the job subtype

## Supported software levels

| Component | Required Version |
|---|---|
| Exigen BatchJobTrigger | 1.0 |
| OpCon | 19.x or higher |
| Java | Embedded (included — no separate Java installation required) |

## Install the connector

To install the Exigen Connector, complete the following steps:

1. Copy the `ExigenConnector-win.zip` file to a temporary directory on the target Windows server (for example, `C:\temp`).
2. Extract the zip file into the desired installation directory.

After extraction, the installation root directory contains the following:

| Item | Description |
|---|---|
| Connector executable | The main connector program |
| `Connector.config` | The connector configuration file |
| `java\` | The embedded Java runtime |
| `wsdl\BatchJobTrigger.wsdl` | The web service definition file |
| `emplugins\` | The Enterprise Manager job subtype plugin |

## Install the job subtype

To install the Exigen job subtype in Enterprise Manager, complete the following steps:

1. Copy the Enterprise Manager plugin file from the `emplugins` directory in the connector installation to the `dropins` directory of your Enterprise Manager installation.

   **NOTE:** If the `dropins` directory does not exist, create it in the Enterprise Manager root directory.

2. Restart Enterprise Manager. The **Exigen** job subtype is available when you select a Windows job type.

   **NOTE:** If the job subtype does not appear after restart, close Enterprise Manager and reopen it using **Run as Administrator**. After this initial launch, you can use Enterprise Manager normally.

3. In OpCon, create a global property named `ExigenPath` and set its value to the full path of the connector installation directory.

## Configure the connector

The `Connector.config` file defines the web service address, endpoint, and WSDL location. To configure the connector, complete the following steps:

1. Open the `Connector.config` file in the connector installation directory.
2. Set the values in the `[EXIGEN]` section to match your Exigen environment.
3. Save the file.

### Configuration options

| Property | Description |
|---|---|
| `CONNECTOR_NAME` | The name of the connector. Do not change this value. |
| `DEBUG` | Enables debug logging. Set to `ON` to capture detailed log output for troubleshooting, or `OFF` for normal operation. Default: `OFF`. |
| `EXIGEN_SERVER_ADDRESS` | The address of the Exigen web server. This value overwrites the web server address in the supplied WSDL file. |
| `EXIGEN_SERVICE_ENDPOINT` | The web service endpoint used when calling the Exigen web service. |
| `EXIGEN_WSDL_LOCATION` | The path to the `BatchJobTrigger.wsdl` file, relative to the installation directory. Do not change this value. |

### Example configuration file

```
[CONNECTOR]
CONNECTOR_NAME=Exigen Connector
DEBUG=OFF

[EXIGEN]
EXIGEN_SERVER_ADDRESS=http://localhost:8080
EXIGEN_SERVICE_ENDPOINT=/localhost/webservices/BatchJobTrigger
EXIGEN_WSDL_LOCATION=wsdl/BatchJobTrigger.wsdl
```

## FAQs

**Can the connector be installed on a server other than the OpCon server?**
Yes. The connector can be installed on the OpCon server, the Exigen application server, or any separate Windows server. If installing on a separate server, an OpCon Windows Agent must be installed on that server.

**Do I need to install Java separately?**
No. The connector includes an embedded Java 1.8 runtime. No separate Java installation is required on the host server.

**What should I do if the Exigen job subtype does not appear in Enterprise Manager after restart?**
Close Enterprise Manager and reopen it using **Run as Administrator**. The subtype should appear after this step. You can use Enterprise Manager normally afterward.

**Where are the log files stored?**
Log files are stored in the `log` directory under the connector installation root (for example, `C:\ExigenConnector\log`).

## Glossary

**BatchJobTrigger** — The Exigen web service used to create and start job groups within the Exigen environment. The connector communicates with this service using the `BatchJobTrigger.wsdl` definition.

**Connector.config** — The configuration file for the Exigen Connector, located in the connector installation root directory. Contains the web service address, endpoint, and WSDL path.

**dropins** — A directory in the Enterprise Manager installation where job subtype plugins are placed. Enterprise Manager scans this directory on startup.

**ExigenPath** — A global property in OpCon that stores the full path to the Exigen Connector installation directory. Used in job definitions to locate the connector executable.

**Related topics:**

- [Overview](./overview.md)
- [Operation](./operation.md)
