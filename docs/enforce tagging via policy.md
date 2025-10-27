# Task 2: Enforce Tagging via an Azure Policy

In this task, I assigned a built-in Azure Policy to enforce resource tagging. The policy will block any resource creation in the resource group that doesn't have the required Cost Center tag, demonstrating governance enforcement.

## Lab Context

- **Policy**: Require a tag and its value on resources
- **Assignment Name**: Require Cost Center tag and its value on resources
- **Target Resource Group**: `az104-rg2`
- **Required Tag**: `Cost Center` = `000`

## Steps Completed

1. **Assign Policy - Basics Tab**
   I navigated to Policy in the Azure portal, selected the "Require a tag and its value on resources" built-in policy definition, and started the assignment process. The Basics tab shows the scope field set to "Azure subscription 1" and the policy definition field populated with the selected policy.
   ![Assign Policy Basics Tab](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/assign%20policy%20basics%20tab.png)

2. **Configure Policy Scope**
   I clicked the ellipsis button next to the Scope field, which opened a scope selector panel. I selected the resource group `az104-rg2` from the Resource Group dropdown to define where the policy will be enforced.
   ![Assign Policy to az104-rg2](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/assig%20policy%20to%20az104-rg2%20.png)

3. **Set Policy Assignment Name and Description**
   I configured the assignment details with the Assignment name "Require Cost Center tag and its value on resources" and added the Description "Require Cost Center tag and its value on all resources in the resource group". The scope now shows "Azure subscription 1/az104-rg2".
   ![Assign Name and Description to Policy](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/assign%20name%20and%20description%20to%20policy.png)

4. **Configure Policy Parameters - Tag Requirement**
   I navigated to the Parameters tab and configured the required tag parameters. I set Tag Name to "Cost Center" and Tag Value to "000". These parameters define the exact tag that must be present on all resources in the resource group.
   ![Tagging Policy with Cost Center Tag](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/tagging%20policy%20with%20cost%20center%20tag.png)

5. **Configure Policy Remediation**
   I reviewed the Remediation tab which explains that this policy assignment will only affect newly created resources. The "Create a Managed Identity" checkbox is unchecked because this policy uses the "Deny" effect and doesn't require a managed identity for enforcement.
   ![Assign Policy Remediation Tab](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/assign%20policy%20remediation%20tab.png)

6. **Review Policy Assignment**
   I reviewed the complete configuration on the Review + create tab. The summary shows all settings including Scope (Azure subscription 1/az104-rg2), Policy definition, Assignment name, Description, and Parameters (Tag Name: Cost Center). Everything is validated and ready to create.
   ![Review and Create Policy](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/reveiw%20and%20create%20policy.png)

7. **Verify Policy Created**
   After clicking Create, I was redirected to the policy definition page. A notification appeared confirming "Creating policy assignment succeeded" for "Require Cost Center tag and its value on resources" in Azure subscription 1/az104-rg2. The notification notes the assignment takes 5-15 minutes to take effect.
   ![Policy Created Overview](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/policy%20created%20overview.png)

8. **Test Policy Enforcement - Attempt to Create Storage Account**
   To test the policy enforcement, I attempted to create a storage account in the `az104-rg2` resource group without adding the required Cost Center tag. I filled in the basic details including subscription, resource group (az104-rg2), and other storage account settings.
   ![Creating Storage Account](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/creating%20storage%20account.png)

9. **Review Validation Error - Summary**
   The deployment validation failed as expected. The Errors panel shows the Summary tab with the error message: "Resource 'az104demostorage001' was disallowed by policy. (Code: RequestDisallowedByPolicy, Policy(s): Require Cost Center tag and its value on resources)". This confirms the policy is actively blocking resources without the required tag.
   ![Summary Error](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/summary%20error.png)

10. **View Raw Error Details**
    I clicked the Raw Error tab to view the detailed JSON error response. The raw error shows the specific policy that blocked the deployment: "Require Cost Center tag and its value on resources" with the policy definition ID and version. This provides complete technical details for troubleshooting policy enforcement.
    ![Raw Error](../screenshots/Enforce%20tagging%20via%20an%20Azure%20Policy/raw%20error.png)

## Key Takeaways

- Azure Policy can enforce governance requirements at deployment time
- The "Require a tag and its value" policy blocks resource creation without the specified tag
- Policy enforcement happens during resource deployment validation
- Built-in policies provide a quick way to implement common governance requirements
- Policy assignments can be scoped to resource groups, subscriptions, or management groups
- Policy assignments take 5-15 minutes to take effect after creation


