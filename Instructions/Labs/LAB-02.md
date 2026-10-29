# Module 2: Create an approval flow with Copilot in Power Automate

## Lab Scenario

In this exercise, you'll automate the approval of real estate showing requests. When an agent adds a showing to the **RealEstateShowings** table that you built in Module 1, a flow sends an approval request, records the decision in the **Is Confirmed** column, and emails the client the result. You'll describe the flow to Copilot in Power Automate, review and complete the actions it generates, add email notifications, and then test the flow end to end by adding a showing in the Real Estate Showings app and approving the request in Outlook.

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1: Create an approval flow with Copilot
- Task 2: Add email notifications and test the flow

### Task 1: Create an approval flow with Copilot

In this task, you'll describe an approval flow to Copilot, and then complete the trigger, the approval, the condition, and the actions that update the row.

1. Open a new browser tab and navigate to Power Automate by copying and pasting the following link:

   ```
   https://make.powerautomate.com
   ```

   > **Note:** If you're asked to sign in, use the following credentials. If a **Pick an account** page appears, select your lab account.
   >
   > - **Email/Username:** <inject key="AzureAdUserEmail" enableCopy="true"/>
   > - **Temporary Access Pass:** <inject key="AzureAdUserPassword" enableCopy="true"/>

1. Power Automate opens in the default environment. In the upper-right corner, select **Environments (1)**, and then under **Build flows**, select **Copilot (2)**, the environment that you created in Module 1.

   ![Screenshot of the Select environment pane with the Environments button and the Copilot environment highlighted](../Media/L2T1S1.png)

1. On the Home page, select **Create with Copilot**.

   ![Screenshot of the Power Automate Home page with the Create with Copilot card highlighted](../Media/L2T1S2.png)

1. On the **Describe it to design it** page, enter the following prompt **(1)**, and then select the **Send** arrow **(2)**.

   ```
   When a row is added to the RealEstateShowing table in Dataverse, start and wait for an approval. If approved, update the same row and set Is Confirmed to Yes. If rejected, update the same row and set Is Confirmed to No.
   ```

   ![Screenshot of the Describe it to design it page with the prompt and the Send arrow highlighted](../Media/L2T1S3.png)

1. Copilot shows a suggested flow with a Dataverse trigger, a **Start and wait for an approval** action, and a **Condition** with an **Upsert a row** action in each branch. Review the outline, and then select **Keep it and continue**.

   ![Screenshot of the suggested flow with the Keep it and continue button highlighted](../Media/L2T1S4.png)

   > **Note:** Copilot might suggest a slightly different flow. If the outline doesn't match, select the **Regenerate** icon next to **Keep it and continue**, or rephrase the prompt.

1. On the **Make sure everything's ready** page, confirm that **Microsoft Dataverse** and **Standard approvals** show a green check mark **(1)**, and then select **Create flow (2)**.

   ![Screenshot of the connections list with the green check marks and the Create flow button highlighted](../Media/L2T1S5.png)

1. The designer opens with your flow on the canvas and the **Copilot** pane on the right. The **Start and wait for an approval** action shows **Invalid parameters**, which you'll fix in the next steps.

   ![Screenshot of the flow designer with the generated flow highlighted](../Media/L2T1S6.png)

   > **Note:** If tips such as **Expand or collapse all actions** or **Drafts and Versioning now available** appear, select **Got it** or **Maybe later** to close them.

1. Select the **When a row is added, modified or deleted** trigger and set the following parameters:

   - **Change type:** Select **Added**.
   - **Table name:** Copilot entered **RealEstateShowing**, which Dataverse doesn't recognize. Select the **X** to clear it, enter **RealEstate** in the box, and then select **RealEstateShowings**.
   - **Scope:** Copilot might enter **4**. Select the **X** to clear it, and then select **Organization**.

     ![Screenshot of the trigger parameters with Change type, Table name and Scope highlighted](../Media/L2T1S7.png)

   > **Note:** The trigger might show the warning **Failed to retrieve dynamic outputs ... Could not find table with name 'RealEstateShowing'** until you select the table from the list.

1. Select the **Start and wait for an approval** action. Open the **Approval type** list **(1)**, and then select **Approve/Reject - First to respond (2)**. More parameters appear.

   ![Screenshot of the Approval type list with Approve/Reject - First to respond highlighted](../Media/L2T1S8.png)

1. In **Title**, enter **New Request for Real Estate Showing**. In **Assigned to**, enter **odl_user**, and then select your lab account from the list.

   ![Screenshot of the Title and Assigned to parameters with the lab account suggestion highlighted](../Media/L2T1S9.png)

   > **Note:** You can also ask Copilot to set parameters, but in testing it added a note to the action instead of filling in the **Title**, so enter the value yourself.

1. In **Details**, enter the following text. Press **Shift+Enter** to start each new line.

   ```text
   A new request for a real estate showing has been created. Please review the details below and approve or reject the request:
   Property:
   Client:
   Client Email:
   ```

1. Place the cursor after **Property:** and select the **Insert data from previous step** (lightning) icon **(1)**. In the search box, enter **Property (2)**, and then select **Property Address (3)**.

   ![Screenshot of the dynamic content list with the lightning icon, the search box and Property Address highlighted](../Media/L2T1S10.png)

1. In the same way, add **Client Full Name** after **Client:** and **Client Email** after **Client Email:**. The **Details** parameter should resemble the following image.

   ![Screenshot of the Details parameter with the Property Address, Client Full Name and Client Email tokens highlighted](../Media/L2T1S11.png)

   > **Hint:** You can also type **/** in a parameter to insert dynamic content.

1. Select the **Condition** action. Copilot already set the condition to the approval **Outcome** **is equal to** **Approve**. Confirm the first row matches the image.

   ![Screenshot of the Condition parameters with the Outcome is equal to Approve row highlighted](../Media/L2T1S12.png)

   > **Note:** If Copilot also added an empty second row, you can leave it. The designer ignores empty rows when you save.

1. On the canvas, under **True**, select the **Upsert a row** action. Like the trigger, it shows an error because the table name is wrong.

   ![Screenshot of the canvas with the Upsert a row action and its error highlighted](../Media/L2T1S13.png)

1. In **Table name**, select the **X** to clear the value, enter **RealEstate**, and then select **RealEstateShowings (1)**. If **Row ID (2)** already shows a **body/PrimaryKeyValue** token, select its **X** to remove it. Select the **Row ID** box, select the lightning icon, enter **RealEstateShowing** in the search box, and then select **RealEstateShowing (3)**, the unique identifier of the row.

   ![Screenshot of the Upsert a row parameters with Table name, Row ID and the RealEstateShowing identifier highlighted](../Media/L2T1S14.png)

1. Open the **Advanced parameters (1)** list, and then select **Is Confirmed (2)**. Press **Esc** to close the list.

   ![Screenshot of the Advanced parameters list with Is Confirmed selected](../Media/L2T1S15.png)

1. In **Is Confirmed**, select **Yes**.

   ![Screenshot of the Upsert a row parameters with Is Confirmed set to Yes](../Media/L2T1S16.png)

1. Under **False**, select **Upsert a row 2 (1)**. Repeat the previous three steps, but in **Is Confirmed**, select **No (2)**.

   ![Screenshot of the Upsert a row 2 action with Is Confirmed set to No](../Media/L2T1S17.png)

### Task 2: Add email notifications and test the flow

In this task, you'll add an email to each branch of the condition, save and test the flow, and then submit and approve a showing request.

1. On the canvas, under the **True** branch, select the **+** icon below **Upsert a row**. In the **Add an action** pane, search for **Send an email (V2)**, and then under **Office 365 Outlook**, select **Send an email (V2)**.

   ![Screenshot of the Add an action pane with the search box and Send an email (V2) highlighted](../Media/L2T2S1.png)

1. In the **Create connection** pane, enter **Office 365 Outlook** as the **Connection name (1)**, and then select **Sign in (2)**. If a **Pick an account** window opens, select your lab account.

   ![Screenshot of the Create connection pane with the Connection name and Sign in highlighted](../Media/L2T2S2.png)

1. The **To** box searches people in your organization. To use a column value instead, select the **Settings** (gear) icon above **To**, and then select **Use dynamic content**.

   ![Screenshot of the To settings menu with Use dynamic content highlighted](../Media/L2T2S3.png)

1. Select the **To** box, and then select the lightning icon **(1)**. Search for **Client Email**, and then under **When a row is added, modified or deleted**, select **Client Email (2)**.

   ![Screenshot of the dynamic content list with Client Email under the trigger highlighted](../Media/L2T2S4.png)

   > **Note:** The list also shows the columns returned by **Upsert a row**. Use the ones under the trigger in this lab.

1. In **Subject**, enter the following text:

   ```
   Your request for a real estate showing has been approved
   ```

1. In **Body (1)**, enter **Good day - Your request for a real estate showing has been approved. Please see below for details.**, and then add the following lines, each with the matching dynamic content from the trigger: **Property:** with **Property Address**, **Client:** with **Client Full Name**, and **Client Email:** with **Client Email**. On a new line, add **Response summary (2)** from the **Start and wait for an approval** action.

   ![Screenshot of the Body editor with the tokens and Response summary highlighted](../Media/L2T2S5.png)

1. The completed action should resemble the following image.

   ![Screenshot of the completed Send an email (V2) action for the approved branch](../Media/L2T2S6.png)

1. Under the **False** branch, select the **+** icon below **Upsert a row 2**, and add another **Send an email (V2)** action. In the **Change connection** pane, select the **Office 365 Outlook** connection that you created.

   ![Screenshot of the Change connection pane with the existing Office 365 Outlook connection highlighted](../Media/L2T2S7.png)

1. Configure **Send an email (V2) 1** in the same way as the first email, but use the following **Subject** and first line of the **Body**:

   - **Subject:** Your request for a real estate showing has been rejected
   - **Body:** Good day - Your request for a real estate showing has been rejected. Please see below for details.

     ![Screenshot of the completed Send an email (V2) 1 action for the rejected branch](../Media/L2T2S8.png)

1. Select the flow name in the upper-left corner, and rename the flow to **Request Approval for Real Estate Showing**.

   ![Screenshot of the flow name box with the new name highlighted](../Media/L2T2S9.png)

1. Select **Save**. When the flow is saved, the message **Your flow is ready to go. We recommend you test it.** appears.

   ![Screenshot of the designer with Save and the confirmation message highlighted](../Media/L2T2S10.png)

1. Select **Test**. In the **Test Flow** pane, select **Manually (1)**, and then select **Test (2)**.

   ![Screenshot of the Test Flow pane with Manually and Test highlighted](../Media/L2T2S11.png)

1. The flow waits for the trigger and shows **To see it work now, perform the starting action.** Leave this tab open.

   ![Screenshot of the flow waiting for its trigger with the message highlighted](../Media/L2T2S12.png)

1. Open a new browser tab and navigate to Power Apps by copying and pasting the following link. Make sure the **Copilot** environment is selected, and then select **Apps**.

   ```
   https://make.powerapps.com
   ```

1. Next to **Real Estate Showings**, select **More commands (...) (1)**, and then select **Play (2)**. The app opens in a new tab. If a **Pick an account** page appears, select your lab account.

   ![Screenshot of the Apps page with More commands and Play highlighted](../Media/L2T2S13.png)

1. In the app, select **+ New** and enter the following values:

   - **Agent Email:** agent12@example.com
   - **Client Address:** 210 Pine Road, Portland, OR 97204
   - **Client Email:** <inject key="AzureAdUserEmail" enableCopy="true"/>
   - **Client Full Name:** Jordan Lee
   - **Price:** 610000
   - **Property Address:** 789 Chestnut Street, Portland, OR 97209
   - **Showing Date:** Any future date and time
   - **Showing Name:** Show L
   - **Status:** Scheduled

   Leave **Is Confirmed** empty, because the flow sets it. When you're done **(1)**, select the check mark **(2)** to save the record.

   ![Screenshot of the new record form with the completed fields and the check mark highlighted](../Media/L2T2S14.png)

   > **Note:** You use your own lab email as the **Client Email** so that the result email arrives in your inbox.

1. Switch to the Power Automate tab. The flow is running and waits at **Start and wait for an approval**.

   ![Screenshot of the running flow with the approval action highlighted](../Media/L2T2S15.png)

1. Open a new browser tab and navigate to Outlook by copying and pasting the following link. If a **Pick an account** page appears, select your lab account.

   ```
   https://outlook.office.com
   ```

   > **Note:** If a **Your privacy matters** message appears, select **Continue**.

1. Open the **New Request for Real Estate Showing** email from **Microsoft Power Automate (1)**, review the details, and then select **Approve (2)**.

   ![Screenshot of the approval email with the email and the Approve button highlighted](../Media/L2T2S16.png)

1. Enter a comment **(1)**, for example **Approved. The agent will confirm the time with the client.**, and then select **Submit (2)**.

   ![Screenshot of the approval email with the Comments box and Submit highlighted](../Media/L2T2S17.png)

1. The email updates to **Approved (1)**, and within a minute the flow sends the **Your request for a real estate showing has been approved** email **(2)**.

   ![Screenshot of the approved request and the new notification email highlighted](../Media/L2T2S18.png)

1. Open the new email. It contains the property, client, and client email from the record, and the approval response summary.

   ![Screenshot of the approved notification email with its body highlighted](../Media/L2T2S19.png)

1. Switch to the Power Automate tab. The message **Your flow ran successfully.** appears, and the **True** branch actions show green check marks.

   ![Screenshot of the completed flow run with the success message and the True branch highlighted](../Media/L2T2S20.png)

1. Select **Back**. If the **Your flow is ready to go** dialog appears, select **Got it**. In **28-day run history**, confirm that the run shows **Succeeded**.

   ![Screenshot of the flow details page with the Succeeded run highlighted](../Media/L2T2S21.png)

1. Switch to the Real Estate Showings app tab and refresh the page. Select the **Show L** record and confirm that **Is Confirmed** is now **True**, which the flow set after the approval.

   ![Screenshot of the Show L record with Is Confirmed set to True highlighted](../Media/L2T2S22.png)

## Summary

In this lab, you have accomplished the following:

- Described an approval flow to Copilot in Power Automate and completed the trigger, approval, condition, and update actions it generated.
- Added email notifications for approved and rejected requests and tested the flow from the Real Estate Showings app.
- Approved a request in Outlook and confirmed that the flow updated the record and notified the client.

### Congratulations! You have successfully completed this lab. Click **Next** to continue to the next lab.
