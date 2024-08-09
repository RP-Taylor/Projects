# Scheduling a Pause of Fabric capacity using Power Automate

## Summary
This project features a Power Automate flow designed to schedule checks on the status of a Fabric capacity using Azure Resource Manager. If the capacity is running, the flow will automatically pause it. The recurrence of this flow can be flexible based on your use case including daily, weekly, multiple times per day.

This flow is an alternative to Azure runbooks available from the Azure runbook module gallery (see https://learn.microsoft.com/en-us/fabric/enterprise/pause-resume#schedule-your-operation)

## Requirements
- A Power Automate license is required as this flow leverages a premium connector, the Azure Resource Manager connector.
  - See https://learn.microsoft.com/en-us/power-platform/admin/power-automate-licensing/faqs for more information. Power Automate offers per user licensing. With this plan, only the account executing the flow needs to have premium licensing.
    - See https://www.microsoft.com/en-us/power-platform/products/power-automate/pricing for pricing information.
- Access to pause/read the created Fabric capacity.
- Ability to retrieve the subscription ID, Azure resource group, and Fabric capacity name for the capacity you will be pausing.
  - See https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id#find-your-azure-subscription for information on identifying the subscription ID.
  - Resource group and Fabric capacity names are visible in the Essentials pane on the Azure Fabric capacity page.

## Installing the Flow and Configuring the Azure Resource Manager Connection in Power Automate
1.	Navigate to Power Automate (https://make.powerautomate.com/). 
2.	Select Import Package.
3.	Choose the packaged flow you downloaded via this GitHub branch to import.
4.	You will need to configure and create the Azure Resource Manager connection. Select the gear under “Related  Resources” if it does not exist yet in your environment.
5.	Select ‘Create New’.
6.	Select ‘New Connection’.
7.	Find and configure ‘Azure Resource Manager’ from the list of available connectors using the search box towards the top right of the browser window.
8.	Refresh the connector in the ‘Import Package’ workflow. You should now be able to select the newly created connector.
9.	Refresh Power Automate in your previous browser tab.

## Updating the Flow Based on your Environment and Use Case Requirements

10.	You will now customize the Power Automate flow. Start by selecting ‘Recurrence’ and editing the intervals, time zones, and other information based on your preferences.
11.	Add your subscription ID to the variable "value" in the second step.
12.	Enter the resource group in the third step's "value. The resource group can be found in Azure by navigating to the page containing the Fabric capacity within the Azure portal.
13.	From the same page (in the Azure Essentials pane on the Fabric capacity), enter the name for the Fabric capacity in the fourth step's "value" (capacity name can be found under “Resource name”). Save and test your flow to ensure it is working correctly.
14.	Save and test your flow to verify the flow is now working.

Your flow is now configured. The flow will run at the times you entered in step 10. This flow will run through the steps verifying if the Fabric capacity is running, and if it the capacity is active, suspend the capacity. Note that if you are using the capacity when the capacity is suspended, you will see errors accessing functionality as the capacity will be suspended. You will need to resume the capacity.

**Disclaimer:** Please ensure you implement error handling and regularly check that the flow is operating correctly and according to the scheduled times. This shared flow is provided without any guarantees of its functionality.

This project is provided “as is” without any warranties or guarantees. The authors are not responsible for any damage or issues that may arise from using this code. Users are encouraged to review and test the code thoroughly before deploying it in a production environment. By using this code, you agree to these terms.
