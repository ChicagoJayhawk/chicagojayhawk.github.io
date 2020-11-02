# Configuring a cluster to run a Windows agent

A Windows agent can run in a Windows cluster environment. A cluster environment is defined as multiple machines working together as one system. The cluster environment provides a level of redundancy that allows other machines to take over when one of the machines in the cluster fails.

The following instructions describe how to configure a two-node cluster environment to run the Windows agent offered by TA.

## Prerequisites
Before installing the agent for Windows on the nodes of a cluster, you must first complete and/or verify the following on each node:

* Verify that the systems on each node are identical
* Verify that the agent machines in each node meet the hardware and software requirements specified in the _Tidal Automation Compatibility Matrix_.
* Verify that the user installing the Windows agent has the specified user rights, including access to the registry on each machine.
* Verify that the cluster group has the following resouce types:
    * Network name
    * IP address
    * Physical disk

## Configuring the Windows agent for a cluster
During configuration, you should complete each step on all machines in the cluster before proceeding to the next step in the procedure, rather than completing all steps on one machine before moving to the next machine.

An agent instance must exist on every node in the cluster before it can be configured to run as a cluster. If, for example, you add a third agent instance to one machine in the cluster, you must add a third instance to all other machines in the cluster before configuring the new instance on the first machine.

To configure the agents:

1. Verify that the cluster works correctly. 

    Check that the cluster software is installed and configured correctly by forcing a failure on a server. Be sure that a failover to another server occurs as intended and that control can be returned to the server that failed. Your Windows Cluster Administrator should help you with this.

1. Install the agent for Windows on the first cluster node. 

    Be sure to install the agent to a non-clustered physical disk on the local machine using the default directory path specified during installation.

    **Caution**: You must install the agent on the same disk drive letter on each cluster node. For example, if you install the agent on the C drive of one node, you must also install the agent on the C drive of the other nodes.

1. Stop the agent if it is running.

    !!! attention
        If an agent instance is configured as part of a cluster, you will not be able to stop the agent. You must stop the agent service.

1. If you are adding an agent instance, add the agent instance to all machines in the cluster (see [Installing Windows agents](../windows-install)). 

    An agent instance must exist on every node in the cluster before it can be configured to run as a cluster. After install the agent instance on each of the nodes in the cluster, you can edit the agent instance to configure it for the cluster.

1. From the Windows **Start** menu, choose **Programs > Tidal Automation > Agent > Instance Manager** to display the Agent Instance Manager.
1. Select the first agent instance; then select the **Edit** button to display the Agent Instance Manager’s configuration.

    If this agent instance is on a node that is configured for a cluster with an existing agent service, the **Run on a cluster group** option is available. If the node is not part of a cluster, this option is unavailable. You cannot proceed any further without verifying with your Windows Cluster Administrator that the node is correctly configured as a member of the cluster.

1. Select the **Run on a cluster group** option to display the cluster configuration fields.
1. In the **Cluster Group** field, select the cluster group to which this agent instance belongs.
1. In the **Physical Disk** field, select the disk where the agent instance resides. 

    All the disks that were created on all of the cluster groups are listed. Be sure to select a disk that exists on the cluster group you selected.

1. In the Work Directory field, enter the pathname to the work directory that was created for the cluster group.

    !!! attention
        This work directory must exist on a shared disk that moves with the active node on a fail-over.

1. In the **Cluster Nodes** field, select the node used by this agent instance. 
1. When the fields are completed, select **Save**.
1. Repeat this procedure for each agent instance.

When each agent instance on each node is configured properly, start each clustered agent instance from its active node using the TA Service Control Manager. Starting the agent instance in the Service Control Manager automatically starts the agent resource in the Windows Cluster Administrator.

