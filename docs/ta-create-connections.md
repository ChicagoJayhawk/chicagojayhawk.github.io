# Creating agent connections

The procedures described in this section are performed in the TA Console.

You can start and stop agents, check agent status, change an agent’s job limit and perform other agent-related tasks in your network at any time as described in this section.

!!! note
    For Windows agents, before starting or stopping the agent, check the agent’s status using the TA Service Manager.

## Defining an agent connection
To define a connection between the agent and the Master:

TBD

## Deleting an agent connection
To delete an agent connection:

1.  From the __Connections__ pane, select the agent to delete.
1.  Select the __Delete__ button on the TA toolbar or press the __Delete__ key on your keyboard.

!!! note
    You cannot delete an agent connection unless you are connected to the Master. You can delete an agent connection that is currently in use, however, jobs that were to run on that agent will be disabled. Those jobs will not run again until you assign them to a valid new agent.

## Modifying agent connections
TBD

### Changing an agent's job limit
You can change an agent’s job limit to specify the number of jobs that can run on it concurrently. You can also control the number of jobs running concurrently using queues. 

To change an agents job limit:

1.  From the __Navigator__ pane, choose Administration > Connections to display the __Connections__ pane with the licensed computers. 
1.  Double-click the agent to edit or select the agent and select the __Edit__ button on the TA toolbar to display the agent’s connection definition. 
1.  Select the __General__ tab if it is not showing. 
1.  In the __Job Limit__ field on the __General__ tab, change the job limit to the desired value.
1.  Select __OK__.

### Changing the name of the computer displayed in TA
TBD

### Changing the machine hostname of the computer
TBD

## Managing agent time zones
You can assign a time zone for agent and adapter connection. By using this new time zone assignment, the master can accurately calculate the time difference between the master and agent without relying on the agent. For example, if the agent time zone is set in Central European Time (CET) and if the master time zone is set in Pacific Standard Time (PST), then the master would accurately calculate the time difference between the master and the agent. This calculation is further used to adjust the job launch time during Daylight saving Time (DST).

### Defining the time zone of an agent
TBD

### Applying agent time zone functionality
TBD


## Enabling and disabling agents
TBD

