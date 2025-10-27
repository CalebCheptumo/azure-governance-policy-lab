# Task 3: Apply Tagging via an Azure Policy

In this task, I replaced the previous "Require" policy with an "Inherit" policy that automatically applies tags from the resource group to child resources. This demonstrates how Azure Policy can not only enforce compliance but also automatically remediate resources by adding missing tags.

## Lab Context

- **Previous Policy**: Require a tag and its value on resources (Deny effect)
- **New Policy**: Inherit a tag from the resource group if missing (Modify effect)
- **Assignment Name**: Inherit the Cost Center tag and its value 000 from the resource group if missing
- **Target Resource Group**: `az104-rg2`
- **Tag to Inherit**: `Cost Center` = `000`

## Steps Completed

1. **View Current Policy Assignments**
   I navigated to Policy | Assignments in the Azure portal to view existing policy assignments. The page shows 2 Total Assignments: 1 Initiative Assignment and 1 Policy Assignment. The current assignment "Require Cost Center tag and its value on resources" is visible in the list.
   ![Policy Assignments Overview](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/policy%20assignments%20overview.png)

2. **Delete Previous Policy Assignment**
   I clicked on the "Require Cost Center tag and its value on resources" policy assignment to open its details. I then clicked "Delete assignment" and confirmed the deletion in the dialog box that appeared, asking "Do you want to delete the policy assignment 'Require Cost Center tag and its value on resources'?"
   ![Delete Require Cost Center Policy](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/delete%20require%20cost%20center%20policy.png)

3. **Select New Policy Definition**
   I clicked "Assign policy" and then clicked the ellipsis button next to Policy definition to open the Available Definitions panel. I searched for "Inherit a tag from the resource group if missing" and selected this built-in policy which uses the Modify effect to automatically add missing tags.
   ![Select Inherit Tag Policy](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/select%20inherit%20tag%20policy.png)

4. **Configure Policy Scope**
   I configured the scope by clicking the ellipsis button and selecting resource group `az104-rg2` from the Resource Group dropdown. The scope is set to "Azure subscription 1/az104-rg2" to ensure the policy applies only to resources in this resource group.
   ![Assign Policy Scope az104-rg2](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/assign%20policy%20scope%20az104-rg2.png)

5. **Set Assignment Name and Description**
   I configured the assignment details on the Basics tab with the Assignment name "Inherit the Cost Center tag and its value 000 from the resource group if missing" and added a matching description. Policy enforcement is set to Enabled.
   ![Assign Policy Basics with Name and Description](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/assign%20policy%20basics%20with%20name%20and%20description.png)

6. **Configure Parameters**
   I navigated to the Parameters tab and set the Tag Name parameter to "Cost Center". This specifies which tag will be inherited from the resource group to child resources that are missing this tag.
   ![Configure Parameters Cost Center](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/configure%20parameters%20cost%20center.png)

7. **Enable Remediation Task**
   I navigated to the Remediation tab and checked "Create a remediation task" to apply the policy to existing resources. I selected "System assigned managed identity" as the Type of Managed Identity with location set to (US) East US. This managed identity is required for the Modify effect to add tags to existing resources.
   ![Remediation Tab Create Remediation Task](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/remediation%20tab%20create%20remediation%20task.png)

8. **Review Policy Configuration**
   I reviewed the complete policy configuration on the Review + create tab, verifying the scope, policy definition, assignment name, description, parameters (Tag Name: Cost Center), and remediation settings before clicking Create.
   ![Review and Create Inherit Tag Policy](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/review%20and%20create%20inherit%20tag%20policy.png)

9. **Verify Policy Assignment Success**
   After clicking Create, notifications appeared confirming the successful creation. The notifications show: "Creating remediation task succeeded", "Creating role assignments succeeded", and "Creating policy assignment succeeded" for "Inherit the Cost Center tag and its value 000 from the resource group if missing".
   ![Policy Assignment Success Notification](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/policy%20assignment%20success%20notification.png)

10. **Create Storage Account to Test Policy**
    To test the new policy, I created a storage account named "az104policydemo" in the `az104-rg2` resource group WITHOUT manually adding any tags. This tests whether the policy will automatically inherit the Cost Center tag from the resource group.
    ![Storage Account with Inherited Tag](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/storage%20account%20with%20inherited%20tag.png)

11. **Verify Deployment Success and Tag Inheritance**
    The deployment completed successfully. The deployment overview shows "Your deployment is complete" for deployment name "az104policydemo_1761543149639" in resource group `az104-rg2`. The storage account was created without any validation errors, demonstrating that the policy allows resource creation.
    ![Deployment Complete](../screenshots/Apply%20tagging%20via%20an%20Azure%20policy/deployment%20complete.png)

## Key Verification

When I navigated to the storage account's overview page, I confirmed that the **Cost Center : 000** tag was automatically inherited from the resource group. This proves the "Inherit" policy successfully applied the tag without manual intervention, unlike the previous "Require" policy which would have blocked the deployment.

## Key Takeaways

- The "Inherit" policy uses the **Modify effect** to automatically add missing tags rather than blocking deployment
- **Remediation tasks** can update existing resources to comply with policy requirements
- **Managed identities** are required for policies with Modify or DeployIfNotExists effects
- The Inherit policy provides a better user experience by automatically fixing compliance issues
- Resources created after policy assignment automatically inherit tags from their parent resource group
- Remediation tasks require additional permissions granted through role assignments

## Comparison: Require vs Inherit Policies

| Feature            | Require Policy (Task 2)    | Inherit Policy (Task 3)      |
| ------------------ | -------------------------- | ---------------------------- |
| Effect             | Deny                       | Modify                       |
| Behavior           | Blocks deployment          | Allows deployment + adds tag |
| User Experience    | Forces manual tag addition | Automatic tag inheritance    |
| Managed Identity   | Not required               | Required                     |
| Existing Resources | No automatic fix           | Can remediate via task       |
