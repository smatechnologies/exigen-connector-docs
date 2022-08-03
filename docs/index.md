---
slug: '/'
sidebar_label: 'Exigen Connector'
---

# Exigen Connector

The Exigen Application is an Insurance package from the EIS group.  The Exigen Connector interacts with the internal scheduler of the Exigen Package starting batch jobs within the Exigen environment and reporting the completion status back to OpCon.   

The connector implementation consists of a Windows batch program that is executed by the Windows Agent. The job definitions are entered as Windows jobs using the Exigen job subtype. When the job is scheduled by OpCon, the definitions are passed as arguments to the Exigen Connector.

The Exigen Connector supports the following job types **CREATE** and **START** which can used be used to communicate with the Exigen application environment.

- CREATE Can be used to define a job group consisting of the defined jobs. Once the job group has been created successfully, the job group is started and monitored for completion and the completion code is returned to OpCon. 
         The jobs in the OpCon definition, must exists within the Exigen repository. It is possible to pass parameter information to the jobs associated with the job group.
- START  Can be used to start a predefined job group. The job group is monitored for completion and the completion code is returned to OpCon. It is possible to pass parameter information to the jobs associated with the job group.  

The job definitions are passed to the Exigen Connector as arguments. The connector uses the BatchJobTrigger.wsdl definition to define the web services end points. 
The job definition information received from OpCon are mapped to the appropriate structures and the web service is then called. 

