# Installing Windows agents

This section explains the requirements and process for installing a Tidal Automation agent on a Windows platform:

- [Rights for installing and running agents](#rights-for-installing-and-running-agents)
- [Installing an agent on Windows](#installing-an-agent-on-windes)
- [Verifying the installation](#verifying-the-installation)

## Rights for installing and running agents
The Windows account must have the following rights to install and run agents:

-   Installation rights
    -   Local adminstration rights
    -   Ability to access COM objects

-   Agent user rights

    Local system or, if running under a domain\user account, must have the following local administration rights

    -   Logon as a service
    -   Logon as part of the operating system
    -   Repalce a process token
    -   Ability to access COM objects

    On machines running Windows 2003 or later:

    -   Bypass traverse checking
    -   Adjust memory quotas for the process

-   Runtime user rights
    -   Logon as a batch job

## Installing an agent on Windows

To install an agent:

1.  Download and extract the Tidal Automation Agent for Windows software from the [Tidal Support Center](https://support.tidalsoftware.com).
1.  Double-click the __Agent_windows_TIDAL Agent.msi__ file. 

    The __Security Warning__ dialog box opens.

1.  Click __Run__. 

    The __Status__ panel opens.

    The __Welcome to the TA Agent Setup__ panel opens.

    !!! note
        If any other agents are running on the machine, a dialog box notifies you that the agent(s) must be stopped before the installation can continue.

1.  Click __Next__. 

    The __Destination Folder__ panel is displayed.

1.  Specify the directory in which to install the TA software using either of the following actions::

    —   Select __Change__ and choose the appropriate file.

    —   Accept the default location at __C:\Program Files (x86)\TIDAL__.

1.  Select __Next__. 

    The __Agent Port Number__ panel opens.

1.  Enter the port number that the agent will listen on. The default port is 5912.
1.  Select __Next__. 

    The __Ready to Install the Program__ panel opens.

1.  Select __Install__.

    !!! warning
        Do not click __Cancel__ once the installation process begins copying files in the __Setup Status__ screen. Cancelling the installation at this point corrupts the installation program.

    You will not be able to install the component without the help of Tidal Support Center. If you decide you do not want to install the component, you must complete the installation and then uninstall.

    The __Setup Completed__ panel displays.

1.  Click __Finish__.

## Verifying the installation

To verify the agent installed successfully:

1.  From the Windows __Start__ menu, choose __All Programs > Tidal Automation > TA Service Manager__ to display the TA Service Manager.
2.  From the __Services__ list, choose __AGENT_1__.

    If the TA Service Manager displays the message _AGENT_1: Running_ at the bottom, then the agent is running and the installation was successful.

!!! note
    If you want to edit the service parameters, click the ![](images/ellipses.png) button to access the Service Configuration dialog box.
