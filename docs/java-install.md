# Installing Java-based agents

Companies often need to provide centralized scheduling and administration of workloads that span multiple machines and multiple locations. TA Master/agent architecture provides that capability.

In the basic TA network, the TA Master uses a centralized database, containing all calendar and job scheduling information. One or more agent machines execute the production schedule. One or more client machines provides the TA user interface or console. The only prerequisite for the master/agent relationship is that the machine acting as the TA Master must be on the same TCP/IP network as the machines serving as agents.

Before installing a Java-based TA agent, backup your files and gather the following information:

* Name of the user who will own the agent
* Port number for the agent
* Directory path for the Java Virtual Machine (JVM)

To install the agent from the command line:

!!! note
    While the installer must be run as the root user, the user who runs the agent service must have read access to the directory in which the agent is installed (**/opt**, by default).

1. Download the Tidal Automation Agent for Linux/Unix software. 
1. Login as root.
1. Copy the **install.sh** and **install.tar** files to your **temp** directory.

    !!! note
        Do not unpack the **install.tar** file. The file will automatically unpack during the installation process.

1. Change the permissions on the install.sh file in the directory to make the file executable:

    `chmod 554 install.sh install.tar`

1. Begin the installation by entering:

    `./install.sh`

    The installation program displays an introductory dialog box.

1. Enter **Y** to continue the installation, and select **Enter**. 

    The **Select the Owner** dialog box opens.

    The top of the screen shows the users defined on the machine. In some cases, you might want to select a user who is not defined on the local machine but is defined as a NIS user allowing the user to install over the network.

1. Enter the name of the user to own the agent.

    !!! note
        Carefully consider which user you use to run the agent. You might want to create a user specifically for this purpose.

1. Press Enter.

1. In the Select the Location panel, enter Y; then select Enter.

    !!! note
        Carefully consider which user to run the agent as. You might want to create a user specifically for this purpose.

    The **Agent Configuration Menu** dialog box opens.

1. Type **1** to select the **Add Instance** option; then select **Enter**. 

    The **Select the Location for the Agent Files** dialog box opens.

1. Enter the information you gathered before beginning installation:

    * Name to call the agent
    * Number of the port the agent should use
    * Directory path for the Java binary files (JVM) 

1. Select **Enter**. 

    A confirmation box displays the information that you entered. 

1. Do either of the following:

    * If the information is correct, press **Enter**.
    * If the information is not correct, type **n**. 
    
        You are prompted again for the name, port number, and directory path for the agent. 
