# Task 4: Configure and Test Resource Locks

In this task, I configured a resource lock on a resource group and verified that the lock prevents deletion. Locks are a governance control that protect resources from accidental changes.

## Lab Context

- Resource group: `az104-rg2`
- Lock name: `rg-lock`
- Lock type: `Delete`

## Steps Completed

1. Opened the resource group and navigated to the Locks blade. Confirmed there were no existing locks.
   ![Locks blade before creating lock](../screenshots/Configure%20and%20test%20resource%20locks/az104-rg2%20overview.png)

2. Created a new lock by selecting Add, then set:

   - Lock name: `rg-lock`
   - Lock type: `Delete` (prevents deletion; read-only would block updates)
     After saving, the new lock appeared in the list.
     ![Lock created rg-lock (Delete)](../screenshots/Configure%20and%20test%20resource%20locks/create%20rg-lock.png)

3. Attempted to delete the resource group to validate the lock behavior. Entered `az104-rg2` to confirm deletion.
   ![Delete confirmation dialog for az104-rg2](../screenshots/Configure%20and%20test%20resource%20locks/delete%20az104-rg2%20overview.png)

4. Verified deletion was denied due to the lock. A notification states the resource group is locked and cannot be deleted, with a link to manage locks.
   ![Deletion denied by lock notification](../screenshots/Configure%20and%20test%20resource%20locks/az104-rg2%20failed%20to%20delete.png)

## Key Takeaways

- Delete locks prevent deletions at the selected scope (resource group or resource).
- Read-only locks prevent both updates and deletions.
- Locks override RBAC permissions—users with delete permissions are still blocked.
- Remove the lock if you intend to delete protected resources.
