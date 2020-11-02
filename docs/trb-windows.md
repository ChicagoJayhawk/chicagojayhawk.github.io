# Troubleshooting
This section provides some troubleshooting help for Windows agents.

## Proper configuration of Windows agents
The Windows agent should have been configured properly at the time of installation but sometimes the configuration is unintentionally changed and causes problems. 

A Windows agent will not operate correctly unless it is configured as follows:

* If the agent is configured to run as Windows user, it must be set up as local to the agent server or a domain user.
* This Windows user must be an administrator on the local machine and have the following four user rights assigned
    * Act as part of the Operating System
    * Logon as a batch
    * Logon as a service
    * Replace a process level token
* All runtime users must have the **Logon as a batch user right** on every Windows server on which the runtime user will run jobs.

    !!! note
        If you have to change any of the above, you should restart the server, as Windows does not always make those changes effective without rebooting.

* In the Client Manager, edit each runtime user (and regular user if those are being used to run jobs) and type the Windows password on the **Passwords** tab of the user’s definition. If a Windows domain is not specified, a runtime user is assumed to be local to the agent where it is running a job.
* Also in the Client Manager, from the main menu, select **Activities>System Configuration** to display the **System Configuration** dialog box and select the **Use Passwords to Run Windows Jobs** option.

After confirming that the agent service has been configured as recommended, run this test job from a command prompt:

```
C:\WINNT\system32\cmd.exe
/c set
```

Look at the output for the **Username** variable to see if the runtime user's name listed. If that is working, then you should be able to run jobs wherever the Windows Authentication is accepted.

## Diagnostics for a Windows agent
To run diagnostics for a Windows agent:

1. Login to the agent console as the same user that the agent service is configured to run.

1. Create a shortcut by right-clicking the Windows Desktop and selecting **New > Shortcut** from the context menu to display the **Create Shortcut** dialog box. 

1. In the **Type the location of the item** field, type the following command path:

    ```
    C:\Program Files (x86)\TIDAL\Agent\bin\TidalAgent.exe" Agent=TidalSAAgent_0 Port=5912 Verbosity=Tidaldebug Debug=Yes
    ```

    !!! note
        Your installation path and port number might be different.

1. Using the Service Control Manager, stop the agent. 

1. Double-click the agent shortcut you created to start the agent in debug mode.

    A window named after the agent displays scrolling messages as the agent does its work. The same data displayed in the window is also logged to the Application Log of the Windows Event Viewer. The system must remain logged on and the agent must continue to run in this Application Mode to gather diagnostics.

It is important to modify the properties for the Application Log so it saves an appropriate amount of data. 

To modify the properties:

1. In the **Event View** tree, select the **Application Log**.

1. Right-click and select the **Properties** option to display the **Application Log Properties** dialog box.

1. In the Log size section, adjust the value in the Maximum log size field.

    The value will vary significantly from agent to agent, depending on the environment and usage. Start with 5-10 megabytes of data and increase as needed. You can configure the Event Viewer to either overwrite the previously written data or stop logging when the log size reaches the maximum size.

To stop diagnostics, close the agent application window and restart the agent from the Service Control Manager.

## Configuring diagnostics for a Windows agent
To configure diagnostics for the Windows agent:

1. Log in to the agent console as an authorized user.
1. Using Service Manager, select the Agent that you wish to use diagnose.
1. Add the following string to the end of the **Path:** field.

    ```
    Debug=high
    ```

1. Select **OK** at bottom of panel and respond yes to the “Would you like to restart the service?” pop-up.

To stop diagnostics, close the agent application window and restart the agent from the Service Control Manager.

## Raising the logging levels for Windows agents
To raise the logging level for a Windows Agent:

1. Open the TA Service Manager on the agent machine.
2. Select the agent in the dropdown.
3. Select on the dots [...].
4. In the **Service** tab, change the path to include the **DEBUG** option to read "DEBUG=HIGH".
5. Select **OK** to save changes.
