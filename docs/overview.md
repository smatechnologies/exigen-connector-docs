---
title: Exigen Connector overview
sidebar_label: Overview
description: "Understand what the Exigen Connector is, how it integrates OpCon with the Exigen insurance platform, and the job types it supports."
tags:
  - Conceptual
  - Automation Engineer
  - System Administrator
  - Getting Started
---

# Exigen Connector overview

## What is it?

The Exigen Connector integrates OpCon with the Exigen insurance platform (EIS Group) by starting batch jobs within the Exigen environment and reporting completion status back to OpCon. The connector runs as a Windows batch program executed by the Windows Agent, allowing OpCon to manage Exigen job processing as part of a larger automation schedule.

- Use this connector when you need OpCon to trigger and monitor Exigen batch jobs alongside other automated processes
- Use this connector when you need completion status from Exigen jobs reported back into OpCon for downstream dependency management
- Use this connector when your Exigen environment exposes batch job execution through the BatchJobTrigger web service

## How the connector works

The Exigen Connector is implemented as a Windows batch program that the Windows Agent executes. Job definitions are entered in OpCon as Windows jobs using the Exigen job subtype. When OpCon schedules a job, the definitions are passed as arguments to the connector.

The connector uses the `BatchJobTrigger.wsdl` definition to define web service endpoints. Job definition information received from OpCon is mapped to the appropriate structures, and the web service is called.

## Supported job types

The Exigen Connector supports two job types that communicate with the Exigen application environment:

| Job Type | Description |
|---|---|
| **CREATE** | Defines a job group in Exigen consisting of the specified jobs, then starts the group and monitors for completion. The jobs must exist in the Exigen repository. Parameter information can be passed to jobs in the group. |
| **START** | Starts a predefined job group in Exigen and monitors for completion. Parameter information can be passed to jobs in the group. |

## Supported software levels

The following software versions are required to use the Exigen Connector:

| Component | Required Version |
|---|---|
| Exigen BatchJobTrigger | 1.0 |
| OpCon | 19.x or higher |
| Java | Embedded Java 1.8 (included with the connector) |

## Connector architecture

The connector runs on a Windows server where an OpCon Windows Agent is installed. It can be installed on the OpCon server, the Exigen application server, or a separate Windows server with an agent installed.

**Related topics:**

- [Installation](./installation.md)
- [Operation](./operation.md)
- [Release notes](./release-notes.md)
