# Operation

The Enterprise Manager includes job subtype definitions for the Exigen Application. The job subtype can be accessed by selecting the Exigen job subtype from the drop down list when the Windows Job Type has been selected. 

## Exigen Job definitions
The Exigen Definition, defines various jobs that can be executed within the Exigen environment using the defined web services. 
These include the **CREATE** and **START** Job Group operations. 

The job definition consists of 2 separate areas, with a general area required by all jobs and specific information required depending on the selected job type (CREATE, START). 

### General Information
The general area contains the following fields:

Field     | Description
--------- | -----------
**User Id**          | Required field, defining the Windows batch user that the connector will be executed under.
**Connector Path**   | Required field that contains the installed location of the Exigen Connector. This consists of a global property value which contains the root installation directory. Default value is **ExigenPath**. If more than one Exigen Connector is installed on the same system, then an additional global property should be defined and the entry in this field updated. 
**Operation**        | Required field that contains the  Cegid operation to execute. Select CREATE or START from the drop down list. Depending which function is selected, additional information can be entered in the appropriate TAB definition.

### CREATE Exigen Operation Information
The Create Job Group TAB is associated with the CREATE operation and is used to define a job group that will be created in the Exigen environment. The names of the jobs to add to the job group are defined and the wait for job completion flag can also be set. It should be noted that the wait for job completion context is the completion of the job group creation and the start of the job group. Once the job group has been started successfully, the job group is monitored for completion. The completion code is then returned to OpCon by the Exigen Connector.

The Create Definition TAB area contains the following fields:

Field     | Description
--------- | -----------
**Job Group Name**          | Required field that defines the name of the job group to create in the Exigen environment.
**Wait for Job Completion** | An indicator to inform the connector to wait for job group successful creation before starting the job group and monitoring for job group completion.  
**Jobs to Add to Group**    | Required field and defines the jobs that must be added to the job group that will be created. The jobs must exist in the Exigen repository. To add a job to the group, enter the job name and select the Add button. To update a job name, select the job in the Job List, modify the name and select the Update button. To remove a job from the select, select the job in the Job List and select the Remove button. 

### START Exigen Operation Information
The Start Job Group TAB is associated with the START operation and is used to define a job group that must be started within Exigen environment. It should be noted that the wait for job completion context is the completion of the start of the job group. Once the job group has been started successfully, the job group is monitored for completion. The completion code is then returned to OpCon by the Exigen Connector.

Field     | Description
--------- | -----------
**Job Group Name**          | Required field that defines the name of the job group to create in the Exigen environment.
**Wait for Job Completion** | An indicator to inform the connector to wait for job group successful creation before starting the job group and monitoring for job group completion.  

### Job Parameters
The Job Parameters TAB is associated with the CREATE and START operations and is used to pass parameters to the jobs within the group. To pass parameters to a job within the job group, the job must be identified and the parameters entered on a single line in name value pairs. 

Field     | Description
--------- | -----------
**Job Name**          | Required field that contains the name of the job that parameters will be defined for.
**Parameters**        | Required field that contains the parameters to be passed to the job in name value pairs. Pairs must be separated by a comma (i.e. name1=value1,name2=value2). To add a parameter definition, enter the information in the Job Name and Parameters fields and select the Add button. To modify a definition, select the definition in the table, then update the values in the Job Name and Parameters fields and select the Update button. To remove a definition, select the definition in the table and select the Remove button.
 
### Failure Criteria
The CREATE and START operations require a Failure Criteria definition. The Exigen returned codes are mapped to the following values.
This means that any other than a zero (0) is considered an error completion.

```
Completion Codes

0	Success.
1	Invalid Request.
2	Invalid Job Parameters.
3	Failed to Execute.
4	Not Executed.
5	Job Group already exists.
6	Job Group does not exist.
7	Job does not exist.

```

## Logging and Job Output
The default logging implemented by the connector consists of a maximum cycle of five log files. The log files contain information about the Exigen Connector and any jobs run by the Exigen Connector. The log files are located in the **'installation root\log'** directory. Information is appended into the log files and any error messages, return codes can be viewed in these log files.


