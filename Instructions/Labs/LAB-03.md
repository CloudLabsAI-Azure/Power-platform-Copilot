# Module 3: Build a basic Power Automate flow in Microsoft Copilot Studio

## Lab scenario

In this exercise, you'll build an agent in Microsoft Copilot Studio that tells users the current temperature for any region they ask about. You'll create an agent and a topic that asks the user for a region, build a Power Automate flow that looks up the current weather with the MSN Weather connector, and then call that flow from the topic. Finally, you'll add a condition that suggests a cold drink when it's warm, and test the agent. This lab shows how agents in Copilot Studio can use Power Automate flows to bring real-time data from external services into a conversation.

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1: Create an agent and a topic
- Task 2: Create a flow
- Task 3: Call the flow from the topic and test it

### Task 1: Create an agent and a topic

In this task, you'll create an agent in the Copilot environment, add a topic with trigger phrases, and ask the user which region they want the weather for.

1. Open a new browser tab and navigate to Microsoft Copilot Studio by copying and pasting the following link:

   ```
   https://copilotstudio.microsoft.com
   ```

   > **Note:** If you're asked to sign in, use the following credentials. If a **Pick an account** page appears, select your lab account.
   >
   > - **Email/Username:** <inject key="AzureAdUserEmail" enableCopy="true"/>
   > - **Temporary Access Pass:** <inject key="AzureAdUserPassword" enableCopy="true"/>

   > **Note:** If the **Find your environments here** tip appears, select **Got it**.

   > **Note:** The screenshots in this lab use the light theme. If Copilot Studio appears dark, select **...** next to your name in the lower-left corner and turn off **Dark mode**. Dialogs follow your browser's theme, so you can also set the browser appearance to **Light**.

1. In the lower-left corner, select the environment name **(1)**, and then select **copilot (2)**, the environment that you created in Module 1. If it isn't listed under **Current environment**, expand **All environments** to find it.

   ![Screenshot of the Switch environment menu with the environment button and the Copilot environment highlighted](../Media/L3T1S1.png)

1. On the Home page, select **Other ways to build**.

   ![Screenshot of the Copilot Studio Home page with Other ways to build highlighted](../Media/L3T1S2.png)

1. Under **Build with standard orchestration**, select **Agent (Standard)**.

   ![Screenshot of the Other ways to build page with the Agent Standard option highlighted](../Media/L3T1S3.png)

   > **Note:** The **Agent** card on the Home page creates an agent that uses skills and tools instead of topics. This lab uses topics, so you create a standard agent.

1. In the **Name your agent** dialog, enter **Check Weather (1)**, and then select **Create (2)**. It takes about a minute to set up the agent.

   ![Screenshot of the Name your agent dialog with the name and the Create button highlighted](../Media/L3T1S4.png)

   > **Note:** If the message **This feature isn't available until your agent has finished setting up** appears, wait until **Your agent has been provisioned** appears.

1. On the agent's page, select **+7 (1)**, and then select **Topics (2)**.

   ![Screenshot of the agent page with the more tabs menu and Topics highlighted](../Media/L3T1S5.png)

   > **Note:** If the **Test your agent** pane is open, you can close it to see more of the page.

1. Select **+ Add a topic**, and then select **From blank**.

   ![Screenshot of the Topics page with Add a topic and From blank highlighted](../Media/L3T1S6.png)

1. In the topic toolbar, select **More**, and then select **Details**.

   ![Screenshot of the topic toolbar with More and Details highlighted](../Media/L3T1S7.png)

1. In the **Topic details** pane, enter **Check Weather** as the **Name**, and then close the pane.

   ![Screenshot of the Topic details pane with the Name highlighted](../Media/L3T1S8.png)

1. In the **Trigger** node, under **User says a phrase**, select **Edit (1)**. In the **Add phrases** box **(2)**, enter the following phrases, pressing **Shift+Enter** after each one, and then select the **Add** icon next to the box.

   ```text
   What is the weather
   What is the temperature today
   Will it rain today
   Is it snowing
   How hot is it
   ```

   ![Screenshot of the Phrases pane with Edit and the five phrases highlighted](../Media/L3T1S9.png)

1. Select an empty area of the canvas to close the pane. The **Trigger** node lists the five phrases.

   ![Screenshot of the Trigger node with the five phrases highlighted](../Media/L3T1S10.png)

1. Below the **Trigger** node, select **Add node (+) (1)**, and then select **Ask a question (2)**.

   ![Screenshot of the Add node menu with Ask a question highlighted](../Media/L3T1S11.png)

   > **Hint:** If the menu is cut off at the bottom of the window, scroll down while the menu is open.

1. In the **Question** node, enter the following text in the message box **(1)**. Then, under **Identify**, select **Multiple choice options**, and in the list, select **User's entire response (2)**.

   ```
   Of course, I can share the weather with you! Can you tell me the name of the region where you want to know the weather?
   ```

   ![Screenshot of the Question node and the Choose information to identify list with User's entire response highlighted](../Media/L3T1S12.png)

1. Under **Save user response as**, select the variable name **Var1 (1)**. In the **Variable properties** pane, change **Variable name** to **Region (2)**, and then close the pane.

   ![Screenshot of the Variable properties pane with the variable name Region highlighted](../Media/L3T1S13.png)

1. Select **Save** in the upper-right corner. The message **Topic Saved!** appears.

   ![Screenshot of the topic with the Save button highlighted](../Media/L3T1S14.png)

### Task 2: Create a flow

In this task, you'll create a Power Automate flow that takes a region from the agent, gets the current weather from MSN Weather, and returns the temperature.

1. Below the **Question** node, select **Add node (+)**, point to **Add a tool (1)**, and then on the **Basic tools** tab, select **Create a flow (2)**.

   ![Screenshot of the Add a tool pane with Add a tool and Create a flow highlighted](../Media/L3T2S1.png)

   > **Note:** Power Automate opens in a new browser tab with a flow template. If the list shows **New Agent flow** instead of **Create a flow**, select it. The agent flow designer opens in the same tab, its trigger is named **When an agent calls the flow** and its last action **Respond to the agent**, and you select **Save draft** and then **Publish** instead of **Save**. The rest of the steps are the same.

1. The designer shows a **When Copilot Studio calls a flow** trigger and a **Return value(s) to Power Virtual Agents** action. Select **When Copilot Studio calls a flow**.

   ![Screenshot of the flow designer with the When Copilot Studio calls a flow trigger highlighted](../Media/L3T2S2.png)

1. Select **Add an input**, and then select **Text**.

   ![Screenshot of the Choose the type of user input options with Text highlighted](../Media/L3T2S3.png)

1. Replace the input name **Text** with **Region (1)**, and leave the second box as it is. Then, select the **Insert a new action (+)** icon **(2)** between the two nodes, and select **Add an action**.

   ![Screenshot of the trigger with the Region input and the Insert a new action icon highlighted](../Media/L3T2S4.png)

1. In the **Add an action** pane, search for **weather (1)**, and then under **MSN Weather**, select **Get current weather (2)**.

   ![Screenshot of the Add an action pane with the search box and Get current weather highlighted](../Media/L3T2S5.png)

1. In the **Create connection** pane, select **Create new** to create a connection for MSN Weather.

   ![Screenshot of the Create connection pane with Create new highlighted](../Media/L3T2S6.png)

1. Select the **Location** box, and then select the **Insert data from previous step** (lightning) icon **(1)**. Under **When Copilot Studio calls a flow**, select **Region (2)**. Leave **Units** set to **Imperial**.

   ![Screenshot of the dynamic content list with the lightning icon and the Region input highlighted](../Media/L3T2S7.png)

   > **Hint:** You can also type **/** in the **Location** box and select **Insert dynamic content**.

1. The **Get current weather** action should resemble the following image.

   ![Screenshot of the Get current weather action with Location set to Region and Units set to Imperial](../Media/L3T2S8.png)

1. Select the **Return value(s) to Power Virtual Agents** action, select **Add an output**, and then select **Number**.

   ![Screenshot of the Choose the type of output options with Number highlighted](../Media/L3T2S9.png)

1. Enter **Temperature (1)** as the output name. Select the **Enter a value to respond with** box, select the **Insert data from previous step** (lightning) icon, and search for **Temperature**. Under **Get current weather**, select **Temperature (2)**.

   ![Screenshot of the dynamic content list with Temperature under Get current weather highlighted](../Media/L3T2S10.png)

1. The output should resemble the following image **(1)**. Select the flow name **Power Virtual Agents Flow Template** in the upper-left corner, replace it with **Get Temperature (2)**, and press **Enter**. Then, select **Save (3)**.

   ![Screenshot of the Return value(s) action with the Temperature output, the flow name and Save highlighted](../Media/L3T2S11.png)

1. When the message **Your flow is ready to go. We recommend you test it.** appears, close the Power Automate tab and return to the Copilot Studio tab.

   ![Screenshot of the saved flow with the Your flow is ready to go message highlighted](../Media/L3T2S12.png)

### Task 3: Call the flow from the topic and test it

In this task, you'll add the flow to the Check Weather topic, add a condition that changes the reply when it's warm, and test the agent.

1. In the Copilot Studio tab, refresh the page (press **F5**) so that the new flow is listed. If the **Test your agent** pane opens, close it.

   > **Note:** The flow isn't added to the topic automatically, so you add it in the next step.

1. Below the **Question** node, select **Add node (+)**, point to **Add a tool (1)**, and then on the **Basic tools** tab, select **Get Temperature (2)**.

   ![Screenshot of the Add a tool pane with Add a tool and the Get Temperature flow highlighted](../Media/L3T3S1.png)

1. In the **Action** node, under **Power Automate inputs**, select the **Select variable** (...) icon **(1)** next to **Enter or select a value**. Notice that the flow's output is already saved in a **Temperature (2)** variable.

   ![Screenshot of the Action node with the Select variable icon and the Temperature output highlighted](../Media/L3T3S2.png)

1. In the **Select a variable** pane, on the **Custom** tab, select **Region**.

   ![Screenshot of the Select a variable pane with the Region variable highlighted](../Media/L3T3S3.png)

1. Select **Save**. The **Action** node now passes **Region (1)** to the flow and saves the result in **Temperature (2)**.

   ![Screenshot of the Action node with the Region input and the Temperature output highlighted](../Media/L3T3S4.png)

1. Below the **Action** node, select **Add node (+)**, and then select **Add a condition**. In the **Condition** branch, select **Temperature** as the variable, select **is greater than**, and enter **75**.

   ![Screenshot of the Condition branch with Temperature is greater than 75 highlighted](../Media/L3T3S5.png)

1. Below the **Condition** branch, select **Add node (+)**, and then select **Send a message**. Enter the following message. To insert a variable, select the **Insert variable** ({x}) icon, search for the variable name, and then double-click the variable.

   - **For** {Region} **the temperature is** {Temperature} **and that is getting warm! Consider cooling off with one of our cold brew coffees.**

     ![Screenshot of the Message node with the warm weather message highlighted](../Media/L3T3S6.png)

   > **Note:** The braces show where to insert a variable. Type a space before and after each variable, otherwise the words run together in the reply.

1. Below **All other conditions**, select **Add node (+)**, select **Send a message**, and enter the following message in the same way:

   - **The temperature for** {Region} **is** {Temperature}**.**

     ![Screenshot of the All other conditions Message node with the message highlighted](../Media/L3T3S7.png)

1. The two branches should resemble the following image.

   ![Screenshot of the Condition branch and All other conditions branch with their messages highlighted](../Media/L3T3S8.png)

1. Below the branches, select **Add node (+)**, point to **Topic management (1)**, and then select **End conversation (2)**.

   ![Screenshot of the Topic management menu with End conversation highlighted](../Media/L3T3S9.png)

1. Select **Save**. The topic ends with an **End conversation** node.

   ![Screenshot of the topic with the End conversation node highlighted](../Media/L3T3S10.png)

1. Select **Test (1)** in the upper-right corner. In the **Test your agent** pane, enter **What is the weather**, and when the agent asks for the region, enter **Seattle**. The agent replies with the current temperature **(2)**.

   ![Screenshot of the Test your agent pane with the Test button and the temperature reply highlighted](../Media/L3T3S11.png)

   > **Note:** If the agent replies **Let's get you connected first**, select **Open connection manager**, select **Connect** next to **MSN Weather**, select **Submit**, and then return to the test pane and select **Retry**.

You have created an agent and a topic in Microsoft Copilot Studio that uses a Power Automate flow to provide real-time data from an external service to the user.

## Summary

In this lab, you have accomplished the following:

- Created a standard agent in Microsoft Copilot Studio and a topic that asks the user for a region.
- Built a Power Automate flow that gets the current temperature from MSN Weather.
- Called the flow from the topic, added a condition to tailor the reply, and tested the agent.

### Congratulations! You have successfully completed this lab. Click **Next** to continue to the next lab.
