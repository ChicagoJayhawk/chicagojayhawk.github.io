# DataMover job support

**Note**: DataMover jobs are only supported on Unix/Linux agents.

## Amazon S3 functionality
The total volume of data and number of objects you can store are unlimited. Individual Amazon S3 objects can range in size from one byte (1 B) to five terabytes (5 TB). The largest object that can be uploaded in a single PUT is five gigabytes (5 GB). For objects larger than 100 megabytes (100 MB), customers should consider using the multipart upload capability.

When using multipart upload, each part must be at least 5 MB in size, except the last part. So, in the list of files provided on the dialog box, each must be at least 5MB other than the last file in the list.

## HFS functionality

### Hortonworks Hadoop
Download the Hortonworks Hadoop client libraries and copy into the **Agent/lib** directory. See [Installing Hadoop client libraries](../app-hadoop/#installing-hadoop-client-libraries), for information about obtaining and installing the libraries.

## Cloudera Hadoop
Download the Cloudera Hadoop client libraries and copy into the **Agent/lib** directory. See [Installing Hadoop client libraries](../app-hadoop/#installing-hadoop-client-libraries), for information about obtaining and installing the libraries.

## MapR Hadoop
To use DataMover for MapR Hadoop, the MapR client must be installed on the machine running the TA agent. The TA agent supports MapR client versions 1.2.9 and 2.0.0. It is the user's responsibility to ensure that the MapR client is installed properly and is communicating with the MapR cluster. For more information on how to set up the MapR client, see:

[http://www.mapr.com/doc/display/MapR/Setting+Up+the+Client](http://www.mapr.com/doc/display/MapR/Setting+Up+the+Client)

No files need to be copied for MapR Hadoop. However, updates to the tagent.ini file are required. See [HFS usage notes](#hfs-usage-notes) for details.


## HFS usage notes

### Agent ini file

#### Kerberos Configuration
If an agent is going to access any Hadoop file system that is secured by Kerberos, the new **Kerberos Realm** and **Kerberos KDC Name** must be specified in the agent's **tagent.ini** file. Like other **tagent.ini** parameters, these values can be specified at a global (all) agent level or on a per agent basis. Unless both of these parameters are defined, the agent will not attempt Kerberos authentication, even if the Hadoop Data Mover Job has checked the **Use Kerberos Authentication** check box.

#### MapR Configuration
When using MapR Hadoop on a 64-bit machine, add the following line to your **tagent.ini** file (assuming the MapR client is installed in the default location):

`jvmpara=-Djava.library.path=/opt/mapr/hadoop/hadoop-0.20.2/lib/native/Linux-amd64-64`

When using MapR Hadoop on a 32-bit machine, add the following line to your tagent.ini file (assuming the MapR client is installed in the default location):

`jvmpara=-Djava.library.path=/opt/mapr/hadoop/hadoop-0.20.2/lib/native/Linux-i386-32`

To use MapR Hadoop, you must also specify the location of the MapR Hadoop jar files. Use the **MapRClasspath** parameter to specify the full path to the required MapR Hadoop jar file directory.

Add the following line to your tagent.ini file (assuming the MapR client is installed in the default location):

`maprclasspath=/opt/mapr/hadoop/hadoop-0.20.2/lib/*`

### User configuration file
With this release of the agent, there is a new user configuration file, TdlUser.cfg, that specifies parameters for the runtime user associated with a job. It is located in the agent's root directory, for example, `/opt/TIDAL/Agent/<name-of-agent>`.

The user configuration file has the following layout:

```
parameter=value 
parameter=value

[user-1] 
parameter=value 
parameter=value
.
.[user-2] 
parameter=value 
parameter=value
```

A parameter value is specified in a parameter/value line which has the form parameter=value. Default configuration parameters to be applied to all users are specified before the first user-specific parameter values, which is referred to as the “default section”. To specify parameter values and/or to override a default parameter value for a particular user, add a section for that user. A user section starts with a "user section" line that contains the user name enclosed in brackets (“[", “]”) followed by a number of parameter/value lines. All parameter/value lines following a user section line up until the next user section line (or end of the file) are applied to that specific user. Parameter values specified in a user section override parameter values that are specified in the default section. Lines that start with the "#" character are ignored.

The new user configuration parameters are **KerberosPrincipal** and **KeyTabFilePath**. These parameters specify the **Principal** and **KeyTab** file for the agent to use when performing Kerberos authentication.
