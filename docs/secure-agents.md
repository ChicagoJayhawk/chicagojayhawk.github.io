# Securing agent and TA Master connections

Each agent includes a **Masters.cfg** file that lets you strictly control which Tidal Automation Master instances can connect to it. You can uniquely identify the specific TA Masters to which a TA agent will create connections by specifying any of the following:

* TA Master alias
* TA Master alias and a specific local TCP/IP address
* TA Master alias, the specific local TCP/IP address, and a global TCP/IP address

The **Masters.cfg** file must be created in the agent’s local directory. This directory is in the install path of the agent and has the name of the agent as it was specified when the agent was defined, similar to the following default locations: 

-   For 32-bit Windows

    ``C:\Program Files\TIDAL\Agent\TIDAL_AGENT_1``

-   For 64-bit Windows 

    ``C:\Program Files(x86)\TIDAL\Agent\TIDAL_AGENT_1``

-   For Unix (Linux, z/OS)

    ``/opt/TIDAL/Agent/TidalAgent1``

-   For OVMS

    ``sys$sysdevice:[tidal.agent.tidalagent1]``

This file should have limited access using native system access control definitions.

<!--
## Agent connect protocol

The following describes the normal connection sequence for an Agent to Master connection to be established.

The Master connects to the Agent well-known port (default 5912, configurable).  The Master sends a registration message to the Agent specifying the Masters IP address and listening port (and some other configuration information).  This connection is then terminated.

For each Master that has registered as above, the Agent will attempt to connect using the information from the registration.  This will happen each time the connection is lost for any reason.

The Agent will attempt to connect to the IP and port provided by the Master in the registration message.  If this fails, the Agent will attempt to connect to the IP obtained from the network as the source IP (may be firewall IP) and the port provided in the registration message.

When the connection is made, the Agent will generate an encryption key based on a random seed.  This encryption key and other configuration information about the Agent will be sent to the Master.  The encryption key is 'wrapped' by a method that the Master knows how to 'unwrap' in order to get the raw key.  This key is used to encrypt the body of all future messages (encryption is a configurable option that is on by default).

-->

## About the Masters.cfg file

The **Masters.cfg** file uses the following structure:

```
[INCLUDE/EXCLUDE]
TA Master alias entry
TA Master alias entry
```

where: 

*   [INCLUDE/EXCLUDE] is an optional statement on the first line of the file that specifies whether to include or exclude connections with the specified TA Master alias entries;

    + INCLUDE: Only the specified TA Masters with optionally specified IP addresses will be connected to by the agent.
    + EXCLUDE: Only the specified TA Masters will be specifically excluded from being connected to by the agent.

    If omitted, the INCLUDE statement is used.

* TA Master alias entry is one of the following forms:

    +   _MasterAlias_

        The _MasterAlias_ typically has the form ES_<<em>hostname-of-master</em>>_1 and is case-insensitive. If specified alone on the line, only the _MasterAlias_ will be verified that it matches what was presented by the TA Master in its registration message.

    +   _MasterAlias_:_IPaddress1_

        For local connections, where the TA Master host machine IP addresses are directly accessible by the agent, you need specify only _IPaddress1_. This address will be verified against the IP address presented by the TA Master in its registration message and the IP address obtained from the network as the origination of the connection that provided the registration message.

    +   _MasterAlias_:_IPaddress1_;_IPaddress2_

        For connections that must traverse a firewall, you must specify a second IP address. _IPaddress2_ will be the externally known address of the firewall. The externally known address of the firewall is what will be obtained by the agent when it retrieves the IP address of the origination of the connection through which the registration message was delivered.

<!--
Optionally, you can use an INCLUDE or EXCLUDE statement on the first line. If specified, these one word entries must be on the first line.  INCLUDE is the default if nothing is specified.

* INCLUDE - only the specified TA Masters with optionally specified IP addresses will be connected to by the agent.
* EXCLUDE - the specified TA Masters will be specifically excluded from being connected to by the agent.

-->

For situations where a TA Master could have multiple IPs, Failover scenarios, or disaster recovery situations, the same MasterAlias can be specified with different IPaddress parameters, similar to the following:

```
INCLUDE
hou-testvm-531:192.168.48.111;172.19.25.125 
hou-testvm-531:192.168.55.211;172.19.25.125
zostest:192.168.95.92          
zostest:192.168.42.92           
catest
```

## Agent connection protocol

The following describes the normal connection sequence for an agent to TA Master connection to be established:

1. The TA Master connects to the agent’s well-known port (default 5912, configurable).  The TA Master sends a registration message to the agent specifying the TA Master’s IP address and listening port (and some other configuration information).  This connection is then terminated.
1. For each TA Master that has registered as above, the agent will attempt to connect using the information from the registration.  This will happen each time the connection is lost for any reason.
1. The agent will attempt to connect to the IP and port provided by the TA Master in the registration message.  If this fails, the agent will attempt to connect to the IP obtained from the network as the source IP (might be firewall IP) and the port provided in the registration message.
1. When the connection is made, the agent will generate an encryption key based on a random seed.  This encryption key and other configuration information about the agent will be sent to the TA Master.  The encryption key is 'wrapped' by a method that the TA Master knows how to 'unwrap' in order to get the raw key.  This key is used to encrypt the body of all future messages (encryption is a configurable option that is on by default).