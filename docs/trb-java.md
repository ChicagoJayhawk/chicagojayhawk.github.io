# Troubleshooting Java-based agents
This section provide troubleshooting help for Java-based agents.

## Proper configuration of Java-based agents
The first line of every Unix agent shell script must adhere to standard Unix scripting guidelines and refer to a shell; for example, **#!/bin/sh**. For more information, refer to your Unix system documentation or consult your System Administrator.

## Diagnostics for a Java-based agent
When a Java-based agent generates errors and doesn’t operate properly, you need to contact the Tidal Support Center to help you resolve the technical issues. However, the Tidal Support Center requires specific information on how the Java-based agent is operating before they can track down the source of the problem. Before contacting the Tidal Support Center about an agent issue, you should enable the following logging settings to collect information about the way the agent is functioning. 

* **ovb=Tidaldebug** to save diagnostic information to the log files
* **debug=y** to save startup information to the files

The Tidal Support Center will ask you to set these values, if you have not done so before contacting them.

To turn on diagnostic logging: 

1. On the agent machine type the following command to stop the agent:

    `./tagent <agent-name> stop`

1. Go to the **/bin** directory and locate the **tagent.ini** file for the desired agent. 
1. Inside the **tagent.ini** file, under the port setting, type the following:

    `ovb=Tidaldebug debug=y`

1. Save the file and its changes.
1. Start the agent:

    `./tagent <agent-name> start`

    Ideally, you want to reproduce the situation that caused the issue so the diagnostics can log what occurred in the system at that time. As soon as the problem reoccurs, contact the Tidal Support Center.

1. Once the problem repeats itself and the diagnostic information is recorded, turn off the agent diagnostics by commenting out the debugging parameter:

    `#ovb=Tidaldebug debug=y`

1. Go to the **Log** directory to get the diagnostic file to send to the Tidal Support Center:

    `cd <agent directory>/<agent-name>/logs`

    Each agent instance has its own directory. The diagnostic files are named `<agent-name>.log` and `<master-server>.log`.

Restarting the agent does not override the recorded information. Though only a small amount of information is normally recorded without the debug parameter, the file will continue to grow in size. You should delete or rename the file after you finish debugging the agent.

!!! note
    Whenever diagnostic logging is being used, you must carefully monitor the amount of disk and database space being consumed. Diagnostic logging can generate large amounts of data and affect system performance.

## Troubleshooting a Java-based agent that fails to start
If your Java-based agent fails to start or hangs on the following message, you might not have any logs to troubleshoot:

```
TIDAL Agent for UNIX
Starting agent testagent on port 5912
Opening Connection......
```

Typically, this problem is caused by an IP address mismatch. Follow the procedure below to check the IP address definitions.

To troubleshoot a Java-based agent that fails to start or hangs:

1. Check the IP of the agent server and how it is configured.
2. Run **ifconfig**.
3. Compare the system IP returned from **ifconfig** to the system's IP defined in the file **/etc/hosts**.
4. Fix any mismatched IP addresses.

## Configuring diagnostics for a Java-based agent
The first line of every Unix agent shell script must adhere to standard Unix scripting guidelines and refer to a shell; for example, **#!/bin/sh**. For more information, refer to your Unix system documentation or consult your System Administrator.

To turn on diagnostic logging: 

1. On the agent machine type the following command to stop the agent:

    `./tagent <agent name> stop`

1. Go to the **/bin** directory and locate the tagent.ini file for the desired agent. 
1. Inside the tagent.ini file, under the port setting, add the following line:

    `ovb=Tidaldebug debug=y`

1. Save the file and its changes.
1. Start the agent:

    `./tagent <agent-name> start`

    Ideally, you want to reproduce the situation that caused the issue so the diagnostics can log what occurred in the system at that time. As soon as the problem reoccurs, contact Tidal Support Center.

1. Once the problem repeats itself and the diagnostic information is recorded, turn off the agent diagnostics by commenting out the debugging parameter:

    `#ovb=Tidaldebug debug=y`

1. Go to the Log directory to get the diagnostic file to send to Tidal Support Center:

    `cd <agent directory>/<agent-name>/logs`

    Each agent instance has its own directory. The diagnostic files are named <FTP>.log, <agent name>.log and <master server>.log.

Restarting the agent does not override the recorded information. Though only a small amount of information is normally recorded without the debug parameter, the file will continue to grow in size. You should delete or rename the file after you finish debugging the agent.

!!! attention
    Whenever diagnostic logging is being used, you must carefully monitor the amount of disk and database space being consumed. Diagnostic logging can generate large amounts of data and affect system performance.

## Raising the logging levels for Java-based agents
To raise the logging level for a Java-based Agent:

1. On the agent machine, go to the agent’s bin directory:

    `cd <agent-home>/bin`

1. Open the tagent.ini file and add the following line in the [config] section:

    ```
    [config]
    ovb=tidaldebug
    debug=y
    ```
    
1. Restart the agent.
