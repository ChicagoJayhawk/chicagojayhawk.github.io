# About agent lists

An agent list is any set of licensed nodes in your network. You can assign jobs to run using agent lists similar to the way you assign them to individual agents. With agent lists, however, you have access to useful functions not available with individual agents. You can specify alternate agent(s) to run your jobs if the primary agent is unavailable, you can balance the workload of many jobs among the agents in the list, or you can broadcast jobs to run on all the machines in the agent list at the same time.

The TA Master does not pick an agent from the agent list assigned to a job until that job is ready to run. Because the agent is not assigned to a job until the last minute, if a user looks at a **Job Details** dialog box before the job runs (e.g., the job is in a **Waiting on Dependencies** state), the **Agent** field on the **Override** tab is empty. The master does not select an agent from the agent list displayed in the **Agent List** field until the job’s dependencies are met and the job is ready to run. Once the job is submitted to run and the agent is selected, the name of the agent displays in the **Agent** field. If the job reruns, the TA Master might assign a different agent from the agent list according to the demands of the production schedule. If you make a change to the **Agent** field, then the **Agent List **field is cleared as you, not the agent list, are selecting the agent.

TA supports Windows, Unix, z/OS (formerly MVS or OS/390) and O/VMS agent platforms, but you cannot combine agents of different platform types in one agent list.

## Types of agent lists

Tidal Automation supports the following types of agent lists:

* **Ordered Agent List**: You can use an ordered agent list to provide alternative agent(s) in case the primary agent is not available when a job is ready to run. When a network or machine failure occurs on the primary agent, the job is automatically routed to the next available alternate agent in the list. Agents are tried in the order that they appear in the list until an operational agent is found. The primary agent is always the first in the list. Alternative agents follow the primary agent.
* **Broadcast**: Simultaneously runs a job on every agent in the list. For example, you might use a broadcast list to backup each machine’s files. 
* **Workload Balancing**: You can use workload balancing to distribute jobs evenly among all the agents in the list. The following agent lists support workload balancing:

    + **Balanced Load**: Launches jobs on the agent which currently has the lightest load. Use this type of list with TA agents on platforms that provide load information.
    + **Balanced Available**: Launches jobs on the agent which currently has the lightest load and job limit available to run the job. Use this type of list with TA agents on platforms that provide load information.
    + **Rotation**: Launches jobs by selecting agents successively. When the end of the agent list is reached, TA starts at the beginning of the list again.
    + **Random**: Launches jobs by selecting agents randomly. Use this type of list to approximate workload balancing with remote shell agents.

## Agent list hierarchies
You can manage agent lists by placing them into hierarchies of parent agent lists and child agent lists. A job using a parent agent list uses all agents belonging to the child agent lists.

Agent list hierarchies provide a convenient way to organize a large set of agents into smaller more manageable sets. When a job is slated to run on an agent list, each child agent list in the parent agent list is treated as if it were a single agent list. For example, in a lightest load agent containing four child agent lists, the child agent list with the lightest load is chosen. The job then chooses among the agents with the lightest load inside the child agent list.

An agent list hierarchy can only consist of agent lists of the same type. For example, you can have balanced load lists under balanced load lists, but not ordered lists under balanced load lists.
