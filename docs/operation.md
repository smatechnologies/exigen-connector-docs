---
title: Operation
sidebar_label: Operation
description: "Configure and run Exigen jobs in OpCon using the Exigen job subtype, including CREATE and START operations, job parameters, and failure criteria."
tags:
  - Reference
  - Automation Engineer
  - Operations Staff
  - Jobs
---

# Operation

## What is it?

The Exigen job subtype in Enterprise Manager provides the fields needed to define and submit Exigen jobs through OpCon. Using the subtype, you can create Exigen job groups from a list of existing Exigen jobs, start predefined job groups, pass runtime parameters to individual jobs within a group, and define failure criteria based on the Exigen completion codes.

- Use the **CREATE** operation when you need OpCon to define a new job group in Exigen, start it, and monitor it for completion
- Use the **START** operation when a job group already exists in Exigen and you need OpCon to start it and monitor it for completion
- Use job parameters when individual jobs within a group require runtime values at execution time

## Exigen job definitions

To create an Exigen job in OpCon, select the **Exigen** job subtype from the list when a Windows job type is selected. The job definition consists of a general area required by all jobs and operation-specific tabs for **CREATE** and **START** jobs.

### General information

The following fields appear for all Exigen job types:

| Field | Required | Description |
|---|---|---|
| **User Id** | Yes | The Windows batch user under which the connector runs. |
| **Connector Path** | Yes | The installation path of the Exigen Connector. Uses the `[[ExigenPath]]` global property by default. If more than one connector instance is installed on the same server, define an additional global property and update this field. |
| **Operation** | Yes | The Exigen operation to run. Select **CREATE** or **START** from the list. The corresponding tab becomes active based on this selection. |

### CREATE operation

The **Create Job Group** tab is associated with the **CREATE** operation. Use it to define a job group that OpCon will create in the Exigen environment, then start and monitor for completion.

**NOTE:** The wait-for-completion setting applies to the job group creation and start sequence. Once the job group starts, the connector monitors the group until it finishes and returns the completion code to OpCon.

The **Create Definition** tab contains the following fields:

| Field | Required | Description |
|---|---|---|
| **Job Group Name** | Yes | The name of the job group to create in Exigen. |
| **Wait for Job Completion** | No | When selected, the connector waits for the job group to be created successfully before starting the group and monitoring for completion. |
| **Jobs to Add to Group** | Yes | The jobs to add to the group. Jobs must exist in the Exigen repository. To add a job, enter the job name and select the **Add** button. To update a job name, select the job in the list, modify the name, and select the **Update** button. To remove a job, select it in the list and select the **Remove** button. |

### START operation

The **Start Job Group** tab is associated with the **START** operation. Use it to start a predefined job group in Exigen and monitor it for completion.

**NOTE:** The wait-for-completion setting applies to the job group start sequence. Once the group starts, the connector monitors it until it finishes and returns the completion code to OpCon.

| Field | Required | Description |
|---|---|---|
| **Job Group Name** | Yes | The name of the predefined job group to start in Exigen. |
| **Wait for Job Completion** | No | When selected, the connector waits for the job group to start successfully before monitoring for completion. |

### Job parameters

The **Job Parameters** tab is associated with both the **CREATE** and **START** operations. Use it to pass runtime parameters to individual jobs within the group.

| Field | Required | Description |
|---|---|---|
| **Job Name** | Yes | The name of the job within the group that will receive the parameters. |
| **Parameters** | Yes | The parameters to pass to the job, in name-value pairs separated by commas (for example, `name1=value1,name2=value2`). To add a parameter definition, enter the job name and parameters and select the **Add** button. To modify a definition, select it in the table, update the fields, and select the **Update** button. To remove a definition, select it and select the **Remove** button. |

## Failure criteria

The **CREATE** and **START** operations require a failure criteria definition. Exigen returns a numeric completion code that the connector maps to an OpCon job status. Any code other than `0` is treated as an error.

| Code | Meaning |
|---|---|
| `0` | Success |
| `1` | Invalid request |
| `2` | Invalid job parameters |
| `3` | Failed to run |
| `4` | Not run |
| `5` | Job group already exists |
| `6` | Job group does not exist |
| `7` | Job does not exist |

## Logging and job output

The connector maintains a rotating set of up to five log files. Log files contain information about the connector and all jobs it runs, including error messages and return codes.

Log files are located in the `log` directory under the connector installation root (for example, `C:\ExigenConnector\log`). Information is appended to the log files as jobs run.

## FAQs

**What is the difference between CREATE and START?**
Use **CREATE** when the job group does not yet exist in the Exigen environment and you want OpCon to define it and run it. Use **START** when the job group already exists in Exigen and you only need OpCon to trigger and monitor it.

**Can I pass parameters to multiple jobs within the same group?**
Yes. Add one entry per job in the **Job Parameters** tab. Each entry associates a job name with its parameter string.

**What does a completion code of 5 mean?**
Code `5` means the job group already exists in Exigen. This typically occurs when a **CREATE** operation is run for a group that was not cleaned up from a previous run.

**How many log files does the connector keep?**
The connector keeps up to five rotating log files. When the maximum is reached, the oldest log file is overwritten.

**What happens if the Exigen web service is unavailable?**
The connector will fail with an error and return a non-zero completion code to OpCon. Check the log files in the `log` directory for details.

## Glossary

**Completion code** — A numeric value returned by the Exigen environment to indicate the result of a job group operation. A value of `0` indicates success; any other value indicates an error.

**CREATE** — An Exigen job operation that defines a new job group in the Exigen environment, adds the specified jobs to the group, starts the group, and monitors it for completion.

**Job group** — A named collection of jobs defined in the Exigen environment. Job groups are the unit of execution triggered by the Exigen Connector.

**Job Parameters tab** — The Enterprise Manager tab used to define runtime parameters passed to individual jobs within an Exigen job group.

**START** — An Exigen job operation that starts a predefined job group in the Exigen environment and monitors it for completion.

**Wait for Job Completion** — A connector setting that controls whether the connector waits for the job group creation or start to complete successfully before monitoring the group for final completion.

**Related topics:**

- [Overview](./overview.md)
- [Installation](./installation.md)
