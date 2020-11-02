# Creating and managing agent lists

You can use the following procedures to create and manage agent lists:

## Adding an agent list
You can add an agent list under a parent agent list of the same type, or under the root platform folder. When you add an agent list under a parent agent list, the parent agent list treats the agent list as if its agents were direct members of the list. 

To add an agent list:

1. From the **Navigator** panel, select **Definitions > Agent** Lists to display the **Agent Lists** panel. 
1. Select a type of agent folder.
2. Select **Add Agent List** from the context menu to display the **Agent List Definition** dialog box. 
3. Specify the properties for the agent list:

    - **List Name**: Unique name for the agent list (60 character limit).
    - **Parent Lis**t: Optional parent list to which you can add this list.
    - **List Type**: Type of agent list based on how you want jobs assigned to agents in the list.

4. Select **OK** to add the agent list. The agent list appears in the **Agent Lists** panel.

## Changing the order of the agents in the list
To change the order of the agents in the list:

1. From the **Navigator** panel, select **Definitions > Agent Lists** to display the **Agent Lists** panel.
1. Select a type of agent folder.
2. For the agent list you want to edit, select **Edit Agent List** from the context menu.
3. In the **Agents Selected** field, select the agent whose position you want to change.
4. Select the up-arrow (^) or down-arrow (v) button(s) to move the agent up or down in the list, or right-click and use the context menu selections to move the agent up or down in the list. 

!!! note
    When specifying an ordered list, the first agent in the list is considered the primary agent. All subsequent agents are alternate agents if the primary agent or other alternate agents are unavailable.

## Deleting an agent list
You can delete an agent list from an **Agent Lists** panel. You cannot delete the platform folder that contains the agent lists. If you delete a parent agent list, you also delete its child agent lists.

To delete an agent list:

1. From the **Navigator** panel, select **Definitions > Agent** Lists to display the **Agent Lists** panel.
1. Select a type of agent folder.
2. Select the agent list to delete and select **Delete** on the TA toolbar, or right-click the agent list and select **Delete Agent List** from the context menu.
3. Select **Yes** in the confirmation dialog to delete the agent list and all its child agent lists (if any) from the TA database.

## Editing an agent list
You can edit an agent list to add or remove agents, to change its name, or to change its parent agent list. You cannot change its platform type or agent list type. Neither can you change its parent to a list of a different type.

To edit an agent list:

1. From the **Navigator** panel, select **Definitions > Agent** Lists to display the **Agent Lists** panel.
1. Select a type of agent folder.
2. Double-click the agent list you want to edit, or right-click the agent list and select **Edit Agent List** from the context menu.
3. Edit the desired properties for the agent list.
4. Click **OK** to update the agent list in the TA database or **Cancel** to discard your changes and close the dialog box.

    The update takes effect the next time the master is refreshed.

## Moving an agent list
You can move agent lists to a different location in the agent list tree, with the following limitations:

* You cannot move agent lists from one platform to another
* You cannotumove agent lists to an agent list of a different list type (Ordered, Random, Balanced Load, Balanced Available, Broadcast, or Rotation)
* You cannot move a parent agent list into one of its own child agent lists.

To move an agent list:

1. From the **Navigator** panel, select **Definitions > Agent** Lists to display the **Agent Lists** panel.
1. Select a type of agent folder.
2. Double-click the agent list you want to edit, or right-click the agent list and select **Edit Agent List** from the context menu.
3. In the **Parent List** field, select a new parent agent list from the drop-down menu.

## Selecting agents for an agent list
You select the agents that belong to an agent list from the **Agent List Definition** dialog box. You can also order the selected list, which is necessary for ordered list types where you can specify the primary agent by placing it first in the list.

To select an agent for an agent list:

1. From the **Navigator** panel, select **Definitions > Agent** Lists to display the **Agent Lists** panel.
1. Select a type of agent folder.
1. Double-click the agent list you want to edit, or right-click the agent list and select **Edit Agent List** from the context menu.
1. From the **Agents Available** field drop-down menu, select the agent(s) to include in the agent list. 

The agents shown in this field are all licensed agents on your system with the specified platform. Note that any agents with a red X are not available for use, although they are licensed agents.

1. To add agents to the agent list, click:

    - The left arrow button (<) to transfer the selected agent(s) to the **Agents Selected** field.
    - The double left arrow button (<<) to transfer all agents to the **Agents Selected** field.

1. To remove agents from the agent list, click:

    - The right arrow button (>) to transfer the selected agent(s) from the **Agents Selecte**d field.
    - The double right arrow button (>>) to transfer all agents from the **Agents Selected** field.

## Displaying agent lists
Agent lists are displayed in a hierarchical format in the agent lists panes. Each platform that TA supports has its own agent lists panel. Each agent list displays its associated agents as child nodes and displays any child agent lists.

To display available agent lists:

1. From the **Navigator** panel, select **Definitions> Agent Lists** to display the **Agent Lists** panel.
2. Select a type of agent folder.

## Displaying agent list properties
To display an agent list’s properties:

1. From the **Navigator** panel, select **Definitions> Agent Lists** to display the **Agent Lists** panel.
2. Select a type of agent folder.
3. Double-click the agent list you want to view, or right-click the agent list and select **Edit Agent List** from the context menu.