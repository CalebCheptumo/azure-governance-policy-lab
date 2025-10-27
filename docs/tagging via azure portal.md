# Task 1: Assign Tags via the Azure Portal

In this task, I created a new resource group and assigned tags to it using the Azure portal. Tags help organize Azure resources with metadata key-value pairs for better management and reporting.

## Lab Context

- **Resource Group**: `az104-rg2`
- **Tag Name**: `Cost Center`
- **Tag Value**: `000`
- **Region**: East US

## Steps Completed

1. **Create Resource Group - Basics Configuration**
   I navigated to Resource groups in the Azure portal and clicked Create. I configured the basic settings with the resource group name `az104-rg2` and selected East US as the region.
   ![Create az104-rg2](../screenshots/Assign%20tags%20via%20the%20Azure%20portal/create%20az104-rg2.png)

2. **Assign Cost Center Tag**
   I navigated to the Tags tab and created a new tag with Name: `Cost Center` and Value: `000`. This tag will be applied to the resource group and can be inherited by child resources.
   ![Assign Cost Center Tag](../screenshots/Assign%20tags%20via%20the%20Azure%20portal/assign%20cost%20center%20tag.png)

3. **Review Resource Group Configuration**
   I clicked Review + Create to validate the configuration. The summary showed the resource group name, region, and the Cost Center tag. Validation passed with a green checkmark.
   ![Review az104-rg2](../screenshots/Assign%20tags%20via%20the%20Azure%20portal/review%20az104-rg2%20.png)

4. **Verify Resource Group Created**
   After clicking Create, I navigated to the resource group overview to confirm `az104-rg2` was successfully created. The Tags section prominently displays the Cost Center tag with value `000`.
   ![az104-rg2 Overview](../screenshots/Assign%20tags%20via%20the%20Azure%20portal/az104-rg2%20overview.png)

5. **Resource Manager View**
   I viewed the resource group in the Azure Resource Manager interface. The Cost Center tag is visible in the metadata section, confirming successful tag assignment and proper resource group governance setup.
   ![Resource Manager Overview](../screenshots/Assign%20tags%20via%20the%20Azure%20portal/resource%20manager%20overview.png)

## Key Takeaways

- Tags help categorize and manage Azure resources
- Resource group tags can be applied during creation or after
- Tags are useful for cost tracking, compliance, and resource management
- Multiple tags can be added to a single resource group


