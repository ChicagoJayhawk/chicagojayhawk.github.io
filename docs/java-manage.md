# Managing Java-based agents

## Starting and stopping agents on Unix

You can start or stop an agent by entering the following commands:

`./tagent <agent name> start`

-or-

`./tagent <agent name> stop`

!!! note "Notes"
    You should stop all Unix agents before rebooting the Unix system. Tidal recommends adding the agent stop command to a Unix system shutdown script to be used when restarting a Unix system.

    When issuing the tagent start command, verify that you are logged on as the user intended to run the agent.

## Checking the status of an agent

To check the agent status on Unix:

1. Run this command:

    `./tagent <agent name> status`

## Preventing unauthorized use of a Unix agent

The Unix agent can be configured to allow only specific users to run jobs on that agent. A list of users can be created to exclude or allow users access to the agent. If an unauthorized user tries to run a job on an agent, the job will end with an “Error Occurred” status.

To exclude users from a Unix agent:

1. Login as the owner of the agent.

1. Create a file called Users.cfg in the agent’s root directory, e.g., **/opt/TIDAL/Agent/<name-of-agent>**.

    !!! note
        The file name, **Users.cfg**, is case sensitive, so only the first letter should be capitalized and the rest of the name should be lower-case.

1. Change the **Users.cfg** file permissions to limit access to just the agent owner, by entering:

    `chmod 700 Users.cfg`

1. In the Users.cfg file, enter:

    `EXCLUDE`

    You alternatively use `INCLUDE` to specify an enumerated list of users.

1. List those users that will be prohibited from accessing the agent. Each user must be on a separate line, as follows:

    ```
    EXCLUDE
    JDegnan
    MCarpent
    TESUser
    ```

If the list of users to exclude is long, enter `INCLUDE` instead of `EXCLUDE`. Then you can list the users to give access to the agent if this is easier.

1. To ensure that the changes take effect, stop and restart the agent.

    -or-

    Disconnect and reconnect the client connection to the agent.

!!! note
    While this procedure prevents unauthorized users from running system commands on an agent for which they are excluded, FTP jobs can still be run from the agent because an user does not login to an agent for FTP access.
