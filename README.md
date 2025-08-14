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

    <img width="707" height="333" alt="image" src="https://github.com/user-attachments/assets/40dbc966-ea02-4acc-8046-33b2512168ad" />

5.	Select ‘Create New’.

    <img width="545" height="461" alt="image" src="https://github.com/user-attachments/assets/53876c6e-1619-425e-bd90-a06ae47b7ccb" />

6.	Select ‘New Connection’.

    <img width="699" height="202" alt="image" src="https://github.com/user-attachments/assets/0b68d022-20b3-44f9-a80f-f3fc49249b39" />

7.	Search and configure ‘Azure Resource Manager’ from the list of available connectors using the search box towards the top right of the browser window.

    <img width="700" height="150" alt="image" src="https://github.com/user-attachments/assets/09304be3-c713-4070-a6a8-63a76f31ec7c" />

    <img width="700" height="263" alt="image" src="https://github.com/user-attachments/assets/a14c7b2b-8539-42b5-802b-0362d6ae07b4" />

    <img width="700" height="106" alt="image" src="https://github.com/user-attachments/assets/03c0769f-4d5d-4e54-aa56-7ef457352121" />

8.	Refresh the connector in the ‘Import Package’ workflow. You should now be able to select the newly created connector.

    <img width="546" height="883" alt="image" src="https://github.com/user-attachments/assets/96b33deb-0b7c-49c8-87a7-5550c9c93ddb" />

9.	Import the now complete package.

    <img width="700" height="407" alt="image" src="https://github.com/user-attachments/assets/e0aa8552-6d5f-49ee-8145-d8213fcecc3a" />

    Before moving onto the next steps, you should see the flow ready for you to configure and customize for your environment. Below is a screenshot of what this screen should look like before moving       forward.
  
    <img width="705" height="403" alt="image" src="https://github.com/user-attachments/assets/53daa4cf-3eca-4822-98a5-293b924d606c" />
    
## Updating the Flow Based on your Environment and Use Case Requirements

10.	You will now customize the Power Automate flow. Begin by selecting Recurrence and configuring the interval, time zone, and other settings to suit your preferences. The interval determines how often the flow runs to check if the Fabric capacity is active (using the previously configured Azure Resource Manager connector). If the capacity is active, the flow will pause it (again using the Azure Resource Manager Connector). For example, to run the process at midnight EST, select the Eastern Time Zone and set the hour to 0. I recommend reviewing the preview to confirm your configuration, as this step serves as the trigger for your flow. For reference, the second screenshot below indicates multiple hours, first at midnight (EST), then at 5pm EST, and then at 9pm EST, where my capacity should be paused if running. See https://learn.microsoft.com/en-us/power-automate/run-scheduled-tasks?tabs=using-copilot for more information on configuring this step.

    <img width="700" height="553" alt="image" src="https://github.com/user-attachments/assets/1d715f30-c94b-4a1f-ba29-6b09301c61fb" />

    <img width="700" height="698" alt="image" src="https://github.com/user-attachments/assets/f521f041-531a-4695-8a37-ec3be41bfb48" />

11.	Add your subscription ID to the variable value in the second step. This information, and the following three steps can easily be viewed and copied via the Fabric capacity in the Azure portal. 

    <img width="1314" height="772" alt="image" src="https://github.com/user-attachments/assets/e6f59ce7-21d2-4b17-8f49-f5b315e8ad67" />
  
12.	Enter the resource group in the third step's value. The resource group can be found in Azure by navigating to the page containing the Fabric capacity within the Azure portal. This is also visible in the Fabric capacity within the Azure portal.

    <img width="1309" height="755" alt="image" src="https://github.com/user-attachments/assets/02a5be00-08d5-4d64-a143-d331b981c2d9" />
    
13.	From the same page (in the Azure Essentials pane on the Fabric capacity), enter the name for the Fabric capacity in the fourth step's value (capacity name can be found under “Resource name”). Save and test your flow to ensure it is working correctly.

    <img width="1309" height="755" alt="image" src="https://github.com/user-attachments/assets/2f0184a8-2fe7-4046-8432-e62b2eed9839" />

14.	Save and test your flow to verify the flow is now working. Be sure to turn on your flow after completeing the above process. Note that this flow is only set to run on the one capacity that you configured above. Other capacities within your environment will need to be seperately configured.

    <img width="630" height="34" alt="image" src="https://github.com/user-attachments/assets/4ceb01fe-39df-495e-88f8-91f7f03a0449" />

Your flow is now configured. The flow will run at the times you entered in step 10. This flow will run through the steps verifying if the Fabric capacity is running, and if it the capacity is active, suspend the capacity. 

It is important to note that if you are using the capacity when the capacity is suspended, you may see errors accessing functionality as the capacity will be suspended. It is important to consider if the Fabric capacity is paused, bursting may cause queued operations to resume when the capacity is restarted when pausing in times of high usage as well as smoothing leading to remaining operations to be summed and added to your Azure bill. See https://learn.microsoft.com/en-us/fabric/enterprise/pause-resume for important information on pausing capacity implications. It is recommended that you use the Fabric capacity metrics app and regularly review cost management shortly after configuring this process to ensure proper and optimized configuration. See https://learn.microsoft.com/en-us/fabric/enterprise/metrics-app and https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/overview-cost-management for more information.

**Disclaimer:** Please ensure you implement error handling and regularly check that the flow is operating correctly and according to the scheduled times. This shared flow is provided without any guarantees of its functionality.

This project is provided “as is” without any warranties or guarantees. The authors are not responsible for any damage or issues that may arise from using this code. Users are encouraged to review and test the code thoroughly before deploying it in a production environment. By using this code, you agree to these terms.

**Disclaimer #2:** This code sample is provided AS IS without warranty of any kind, and should not be interpreted as an offer or commitment on the part of Microsoft, and Microsoft cannot guarantee the accuracy of any information presented. MICROSOFT MAKES NO WARRANTIES, EXPRESS OR IMPLIED, IN THIS CODE SAMPLE.
