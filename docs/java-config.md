# Configuring Java-based agents


- [Adding an agent instance](#addding-an-agent-instances)
- [Modifying an agent instance](#modifying-an-agent-instance)
- [Deleting an agent instance](#deleting-an-agent-instance)
- [Configuring agent parameters](#configuring-agent-parameters)

## Adding agent instances

You can configure Unix agents (add and delete agent instances) using the **Agent Configuration Menu**. 

!!! note
    While the installer must be run as the root user, the user who runs the agent service must have read access to the directory in which the agent is installed (**/opt**, by default).

To display this menu:

1. Log on as agent owner on the agent machine.
1. Go to the **bin** directory by entering:

    `cd /opt/TIDAL/Agent/bin`

1. Type in the following:

    `./tagent config`

    The **Agent Configuration Menu** opens.

## Deleting agent instances

To add an instance:

1. In the **Agent Configuration Menu**, enter **1**; then select **Enter**.
2. Enter the name of the agent, its port number, and the directory path to the Java binaries; then select **Enter**.
3. Select **Y**, then **Enter**, to add the agent instance.
4. Start the agent by entering the following shell command:

    `./tagent <agent name> start`

## Configuring agent parameters

You can configure the parameters of an agent by changing the parameter values in the **tagent.ini** file. The **tagent.ini** file is located in the Unix agent directory. If the default location was used during the agent installation, the agent files are located at **/opt/TIDAL/Agent/bin**. 

Following is an example of a **tagent.ini** file:

```
# =============================================
# Agent Configuration Information
# ===========================================
[config]
agents=sun02,sun11,aix02,test
degbug=yes
ovb=tidaldebug
java=/usr/bin/
#sslvldcrt=n
sshvldhst=/home/secure/prd2_id_rsa.pub
sslvldhst=/home/secure/vvm1.pem

[test]
port=5915
java=/usr/j2rel.4.2_06/bin
minmem=32
maxmem=64
logdays=5

[sun02]
port=5915
java=/usr/j2rel.4.2_06/bin
sslvldcrt=n

[sun11]
port=5915
encryptonly=y

[aix02]
port=5915
java=/usr/java5_64/bin
sslvldcrt=/home/secure/host.crt
ulimitold=y
```

Restart the agent after modifying any of the agent’s parameters. 

You can set the following agent parameters.

<TABLE>
    <TR>
        <TH ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226028"></A>Parameter</P>
        </TH>
        <TH ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226030"></A>Description</P>
        </TH>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226032"></A>agtresource</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226034"></A>Options for monitoring the following agent resources at specified time
                intervals, in milliseconds (default=15000):</P>
            <UL>
                <LI>
                    <A NAME="pgfId-1226159"></A><b>CPU</b>: Monitors CPU usage</LI>
                <LI>
                    <A NAME="pgfId-1226160"></A><b>VMEM</b>: Monitors virtual memory usage</LI>
            </UL>
            <P>
                <A NAME="pgfId-1226161"></A>Setting this parameter takes the following forms:</P>
            <UL>
                <LI>
                    <A NAME="pgfId-1226162"></A><b>agtresource=CPU;VMEM</b>: Montors both resouces at the default 15-second intervals.</LI>
                <LI>
                    <A NAME="pgfId-1226163"></A><b>agtresource=CPU,10000</b>: Monitors only CPU usage at 10-second intervals.</LI>
                <LI>
                    <A NAME="pgfId-1226164"></A><b>agtresource=CPU,10000;VMEM,20000</b>: Monitors CPU usage at 10-second intervals and virtual memory usage at 20-second intervals.</LI>
            </UL>
            <P>
                <A NAME="pgfId-1226165"></A>The minimum interval is 5000 milliseconds, or 5 seconds.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226036"></A>cpuload</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226244"></A>Whether to send agent system load information to the TA Master.</P>
            <UL>
                <LI>
                    <A NAME="pgfId-1226245"></A><b>
                        y</b>
                    : Send load information to the TA Master at one-minute intervals.</LI>
                <LI>
                    <A NAME="pgfId-1226246"></A><b>
                        n</b>
                    (default): Send no information.</LI>
            </UL>
            <P>
                <A NAME="pgfId-1226247"></A><b>Note</b>: Enabling this parameter is typically useful only when an Agent List Definition sets the <b>List Type</b> field to a balanced option, as described in <a href="../agent-lists-about#types-of-agent-lists">Types of agent lists</a>.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226040"></A>debug</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226042"></A>Whether to enable low-level debugging of agent activity. Set the value to
                <b> y</b> to enable debugging.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226044"></A>encryptonly</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226046"></A>Whether to disable agents connections to any TA Master than disables message
                encryption. Valid values include N (default) and Y.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226048"></A>fp</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226525"></A>Pathname of a file that defines environment variables for an agent instance,
                in the form: <b>fp=/folder/file</b>.</P>
            <P>
                <A NAME="pgfId-1226526"></A>Each agent instance can be assigned its own environment file and its
                associated environment variables with their various values. Each variable specified in the environment
                file should follow a <b>variable=value</b> format as in the following examples:</P>
            <P>                
                <code>
                TZ=CST<br>
                SchedulerT=1<br>
                PATH=/usr/sbin
                </code>
                </P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226052"></A>ftptimeout</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226054"></A>Timeout, in milliseconds, for an FTP connection. Setting the value to 0
                results in no timeout for the connection.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226056"></A>homedir</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226583"></A>Whether to use the agent’s home directory or the runtime user’s home
                directory as the working directory:</P>
            <UL>
                <LI>
                    <A NAME="pgfId-1226584"></A><b>
                        y</b>
                    : Uses the runtime user’s home directory.</LI>
                <LI>
                    <A NAME="pgfId-1226585"></A><b>
                        n</b>
                    or omitted (default): Uses the agent’s home directory (where the agent software is installed).</LI>
            </UL>
            <P>
                <A NAME="pgfId-1226586"></A><b>
                    Note</b>
                : Enabling this parameter overrides the working directory setting in the TA Master for all jobs to use
                the user’s home directory.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226060"></A>java</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226062"></A>Pathname for the Java software.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226064"></A>jobkillwait</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226066"></A>Time interval, in seconds, between sending a SIGTERM warning that a Unix job
                is about to be aborted and sending the SIGKILL signal to abort the job. Default: 5 seconds.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226068"></A>jobstopwait</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226070"></A>Time interval, in seconds, between sending a SIGSTP warning that a Unix job
                is about to be put on hold and sending the SIGSTOP signal to pause the job. Default: 1 second.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226072"></A>logdays</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226074"></A>Number of days to preserve log files.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226080"></A>minmem/maxmem</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226082"></A>Minimum and maximum RAM, in MB, to allocate for agent processes. Defaults:
                minmem=16. maxmem=48.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226088"></A>multiftpstd</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226875"></A>How to handle FTP multi-file MGET, MPUT, or MDELETE actions that operate on
                no files. Values include:</P>
            <UL>
                <LI>
                    <A NAME="pgfId-1226876"></A><b>
                        Y</b>
                    (default): Allow the job to complete without reporting errors.</LI>
                <LI>
                    <A NAME="pgfId-1226090"></A><b>
                        N</b>
                    : Allow the job to complete abnormally if the actions operated on no files.</LI>
            </UL>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226769"></A>ovb</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226771"></A>Whether to enable maximum level of debug logging for agent activity. Set the
                value to <b>
                    tidaldebug</b>
                to enable this logging.</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226765"></A>profile</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226903"></A>Whether to override the <b>
                    For Unix, source user’s profile</b>
                setting on the <b>
                    Options</b>
                tab of the <b>
                    Job Definition</b>
                dialog box:</P>
            <UL>
                <LI>
                    <A NAME="pgfId-1226904"></A><b>
                        y</b>
                    : Causes the runtime user profile to be used for all jobs run on the agent.</LI>
                <LI>
                    <A NAME="pgfId-1226905"></A><b>
                        n</b>
                    or omitted (default): Causes the runtime user profile to be used only for jobs whose definitions
                    enable the setting.</LI>
            </UL>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226761"></A>sftpumask</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226763"></A>Permission mask (4-digit octal) for files created on a Unix-based system
                with the <b>
                    SFTP PUT</b>
                actions. Default=<b>
                    0022</b>
                .</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226757"></A>sshvldhst</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226983"></A>
                    Location of SSH host key file.</b>
            </P>
            <P>
                <A NAME="pgfId-1226984"></A>For SFTP host validation, the location of the file containing the public
                keys for the servers that SFTP connections will be established with.</P>
            <P>
                <A NAME="pgfId-1226985"></A>The host key file provides a list of hosts and their associated public keys.
                The format of the file is similar to that used in OpenSSH. Each line contains the name of a host
                followed by its IP address (separated by a comma), the type of key it has, and its key (in base-64
                printable form). For example: </P>
            <P CLASS="Ex1-Example1">
                <A NAME="pgfId-1226986"></A>
                <code>
                jackspc,192.168.1.1 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAIE...
                </code>
            </P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226753"></A>sslvldcrt</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1227009"></A>Whether to disable FTPS SSL certificate validation by Tidal Automation
                agents. Default=<b>
                    Y</b>
                .</P>
            <P>
                <A NAME="pgfId-1227013"></A>Tidal Automation agents validate the host defined in FTPS SSL certificate.
                This host validation feature can be disabled by specifying a <b>
                    SSLVLDCRT</b>
                parameter on the agent command line. The default is SSLVLDCRT=Y (yes). You can turn this off by
                specifying <b>
                    SSLVLDCRT=N</b>
                .</P>
        </TD>
    </TR>
    <TR>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1226749"></A>sslvldhst</P>
        </TD>
        <TD ROWSPAN="1" COLSPAN="1">
            <P>
                <A NAME="pgfId-1227030"></A>
                    Location of file containing host certification key file.
            </P>
            <P>
                <A NAME="pgfId-1227031"></A>For FTPS host validation, the location of the file containing the public
                host certificates (generally self-signed), if not authenticated through a certificate authority.</P>
            <P>
                <A NAME="pgfId-1227032"></A>The certificates in the file must be of the OpenSSL PEM format and be
                bracketed as follows: </P>
            <P>
                <A NAME="pgfId-1227033"></A>
                <code>
                    -----BEGIN CERTIFICATE-----<br>
                    ... first certificate ...<br>
                    ... second certificate ...<br>
                    -----END CERTIFICATE-----<br>
                </code>
            </P>
        </TD>
    </TR>
</TABLE>