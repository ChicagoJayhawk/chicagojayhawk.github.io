# Managing Windows agents

The Service Manager allows you to manage installed agents, including:

* Starting and stopping Windows agents
* Configuring a cluster to run the Windows agent
* Uninstalling Windows agents

## Starting and stopping agents
To start or stop an agent:

1.  From the Windows __Start__ menu, choose __All Programs > Tidal Automation > TA Service Manager__ to display the Service Manager.
1.  From the __Services__ list, choose the name of the agent.
1.  Do either of the following:
    -   Click __Start__ to start the agent.
    -   Click __Stop__ to stop the agent.

## Checking agent status
To check the status of an agent:

1. From the Windows **Start** menu, choose **All Programs > Tidal Automation > Service Manager** to display the Service Manager.
2. From the **Services** list, choose the name of the agent.

    The status of the agent is displayed at the bottom of the manager.

## Configuring jobs to run in the foreground
Because job processes do not normally require user interaction, they usually run in the background on the agent machine. If needed, you can configure your agent’s system to run job processes in the foreground. Running processes in the foreground both allows user interaction with the process as it runs and enables more processes to run by providing another desktop. You can configure the agent through the Service Manager or by editing the Windows registry.

!!! danger
    Changing settings in the Windows registry can have serious consequences on your computer system. Consult with your Windows system administrator before making any registry changes.

If you want to interact with the process, you can configure the job to run in a command prompt window. 

1.  Navigate to **Service Manager > Service Configuration**.
1.  Select the **Run as LocalSystem** and **Allow Service to Interact with Desktop** check boxes, respectively.
1.  Do one of the following:
    -   For 64-bit systems, open regedit and navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Tidal Software` registry setting. 
    -   For 32-bit systems, navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\TIDAL Software\Agent` registry setting.
1.  Right-click **Tidal Software** and select **New > Key**.
1.  Add a new key with the agent name, such as **TIDAL_AGENT_1**.

    Under **TIDAL_AGENT_1**, create a new string called **JobLaunchMode** with assign one of the following values to configure the appearance of the command prompt window:

    * 0 = Hides the command prompt window and activates another window.
    * 1 = Activates the command prompt window and displays it minimized. 
    * 2 = Activates the command prompt window and displays it in its current size and position.
    * 3 = Activates the command prompt window and displays it at maximum size.
    * 4 = Activates the command prompt window and displays it at minimized size.
    * 5 = Displays the command prompt window in its current size and position but the window is not activated.
    * 6 = Displays the command prompt window at its most recent size and position but the window is not activated.
    * 7 = Activates and displays a window at its original size and position. Recommended when displaying the command prompt window for the first time.

1.  In the Job on the **Run** tab, select **Use Password to Run Windows Jobs**.
1.  In the Job on the **Options** tab, select **For UNIX, source users profile**.
1.  In **Runtime Users**, set the **Windows/FTP/Datamover** password for the **Runtime Users**.
1.  Log onto the agent server as the runtime user.

If needed, you can repeat this procedure for the other agent instances that are listed in this key.

To revert back to the original configuration, delete the registry key that was added.

To run the process in the foreground without interacting with the job, you can run it from the default desktop.

## Configuring jobs to run from the default desktop
To run a job from the default desktop:

If you want to interact with the process, you can configure the job to run in a command prompt window. 

1.  Navigate to **Service Manager > Service Configuration**.
1.  Select the **Run as LocalSystem** and **Allow Service to Interact with Desktop** check boxes, respectively.
1.  Do one of the following:
    -   For 64-bit systems, open regedit and navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Tidal Software` registry setting. 
    -   For 32-bit systems, navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\TIDAL Software\Agent` registry setting.
1.  Right-click **Tidal Software** and select **New > Key**.
1.  Add a new key with the agent name, such as **TIDAL_AGENT_1**.

    Under **TIDAL_AGENT_1**, create a new string called **JobUseDefDesktop** with assign one of the following values to configure the appearance of the command prompt window:

    * 0 = Hides the command prompt window and activates another window.
    * 1 = Activates the command prompt window and displays it minimized. 
    * 2 = Activates the command prompt window and displays it in its current size and position.
    * 3 = Activates the command prompt window and displays it at maximum size.
    * 4 = Activates the command prompt window and displays it at minimized size.
    * 5 = Displays the command prompt window in its current size and position but the window is not activated.
    * 6 = Displays the command prompt window at its most recent size and position but the window is not activated.
    * 7 = Activates and displays a window at its original size and position. Recommended when displaying the command prompt window for the first time.

1.  In the Job on the **Run** tab, select **Use Password to Run Windows Jobs**.
1.  In the Job on the **Options** tab, select **For UNIX, source users profile**.
1.  In **Runtime Users**, set the **Windows/FTP/Datamover** password for the **Runtime Users**.
1.  Log onto the agent server as the runtime user.

## Configuring a Windows agent to be a remote job adapter proxy

### Designating the HTTPS port
To designate the HTTPS port:

1. From the Windows **Start** menu, choose **All Programs > Tidal Automation > TA Service Manager** to display the TA Service Manager.
2. Select the <IMG SRC="ellipses.png" ALIGN="BASELINE" ALT=""> button to display the **Service Configuration** dialog box.
3. In the Path field, edit the command line of the agent by entering the following parameter:

    `RJAPort=PPPPP`

    Where **PPPPP** (e.g. **50001**) is the port number you want to use for the HTTPS connection from the adapter.

    For example:

    `"C:\Program Files\TIDAL\Agent\Bin\TidalAgent.exe" AGENT=TIDAL_AGENT_1 PORT=5912 PATH="C:\Program Files\TIDAL\Agent" RJAPort=PPPPP`

1. Select **OK**.
2. Allow Service Manager to restart the agent when you save the change.

!!! note "Notes"
    The proxy support will not be available in this agent if the RJAPort is not specified in the command line. The agent will not be usable by the Adapter until the RJAPort parameter is specified.

    After adding the RJAPort parameter, you will need to add another dependency to the agent service definition called HTTP SSL. You can do this by going into Service Manager and selecting the ellipses (...) for the specific agent, selecting the 'Dependencies' tab, and then selecting 'HTTP SSL' as a new dependency.  The agent will not start automatically at system start-up with-out adding this dependency.(May not be available in Windows 2008 and beyond).

### Assigning a certificate to the HTTPS port
If your machine already has a valid server certificate, you should only have to perform Steps 4 and 5 below.

To create a self-signed host certificate and configure it to a port:

1. Open a DOS prompt (Command Shell).
    1. From the Windows Start menu, choose Run..
    1. In the Run dialog box, enter cmd.
    1. Select OK.

1. Enter the following to create and install a self-signed certificate in the certificate store:

	`makecert -r -pe -n "CN=localhost" -eku 1.3.6.1.5.5.7.3.1 -ss my -sr localMachine -sky exchange` 

    !!! tip
        The **makecert** command is available in the SDK if you have Visual Studio 2005 installed (**Microsoft Visual Studio 8\SDK\v2.0\Bin**).  There are other ways to get a certificate, Google will give you several options.

1. Start **Microsoft Management Console** (mmc) and copy the certifcate  "local" located in **Personal > Certificates into Trusted Root Certification Authorities > Certificates**.

1. At the DOS prompt (Command shell), run either the httpcfg.exe (pre-2008 systems) or netsh (post-2008 systems) command.

    !!! note
        The port used to connect from the Master to the proxy agent via HTTPS (the RJAPORT) must be configured to use SSL.

    _For pre-2008 systems_:

	`httpcfg.exe set ssl -i 0.0.0.0:PPPPP -c "Root" -h XXXXX`

    where **0.0.0.0:PPPPP** is the IP and port. This is for **https://localhost:PPPPP**, where **XXXX** is the thumbprint value of the local certificate. 

    To obtain the thrumbprint of a certificate, open the certificate and select the **Details** tab.  Copy the thumbprint and delete all blanks (spaces) between numbers in the thumbprint.

    !!! note
        The name after **-c** option in the **httpcfg set** command must match the certificate store, Tidal recommends using Root (see below).

    Store Names:

    * **AddressBook**: The X.509 certificate store for other users.
    * **AuthRoot**: The X.509 certificate store for third-party certificate authorities (CAs).
    * **CertificateAuthority**: The X.509 certificate store for intermediate certificate authorities (CAs).
    * **Disallowed**:The X.509 certificate store for revoked certificates.
    * **My**: The X.509 certificate store for personal certificates.
    * **Root**: The X.509 certificate store for trusted root certificate authorities (CAs).
    * **TrustedPeople**: The X.509 certificate store for directly trusted people and resources.
    * **TrustedPublisher**: The X.509 certificate store for directly trusted publishers.

    _For post-2008 systems_:

    `netsh http add sslcert ipport=0.0.0.0:PPPPP certhash=XXXX  appid={YYYYYY}`

    where

    - **ipport=0.0.0.0:PPPP**P (e.g. **0.0.0.0:5000**1) is IP and port used for the URL, as in **https://localhost:PPPPP**.
    - **certhash=XXXX** is the Thumbprint value of the local certificate. 
    
        To obtain the thrumbprint of a certificate, open the certificate and select the **Details** tab. Copy the thumbprint and delete all blanks (spaces) between numbers in 'Thumbprint'.

    - **appid={YYYYYY}** is a GUID identifying the owning application.

1. Select OK.


