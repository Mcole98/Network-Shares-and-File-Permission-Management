# Microsoft Azure Lab: Configuring Network File Shares and Permissions

## Overview
This lab will guide you through configuring network file shares and setting permissions on Microsoft Azure. The focus is on understanding how to control access to shared folders using file share configurations and Active Directory security groups.

### Prerequisites
1. Access to the **DC-1** virtual machine (VM) with domain administrator privileges (`mydomain.com\admin_user`).
2. Access to the **Client-1** VM using a standard domain user account (`mydomain\user_account`).
3. A preconfigured Active Directory environment with **DC-1** and **Client-1**.

---

## Lab Instructions

### Step 1: Create File Shares with Different Permissions
1. **Log into DC-1** using the domain administrator account `mydomain.com\admin_user`.
2. Create the following four folders in the `C:\` drive:
   - `read-access`
   - `write-access`
   - `no-access`
   - `finance`

3. Configure the following permissions for each folder:
   - **Folder:** `read-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read`
   
   - **Folder:** `write-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read/Write`
   
   - **Folder:** `no-access`  
     **Group:** `Domain Admins`  
     **Permission:** `Read/Write`

   - **Folder:** `finance`  
     *(Permissions will be configured later.)*

---

### Step 2: Test Access as a Standard User
1. **Log into Client-1** using a standard user account (`mydomain\user_account`).
2. Open the **Run** dialog (`Windows Key + R`) and enter `\\dc-1` to view shared folders.
3. Attempt to access each shared folder:
   - Which folders are accessible?
   - Which folders allow file creation?

---

### Step 3: Create a Security Group and Configure Permissions
1. **Log back into DC-1** as the domain administrator.
2. Open **Active Directory Users and Computers** and create a security group named `FINANCE_TEAM`.
3. Assign permissions for the `finance` folder:
   - **Folder:** `finance`  
     **Group:** `FINANCE_TEAM`  
     **Permission:** `Read/Write`

4. **Test access on Client-1:**
   - Log in as `user_account` and try to access `\\dc-1\finance`. 
   - Expected result: Access should be denied.

5. **Add User to the Security Group:**
   - On **DC-1**, add `user_account` as a member of the `FINANCE_TEAM` security group.

6. **Re-test Access:**
   - Log out of **Client-1** and log back in.
   - Try accessing the `finance` folder again. 
   - Expected result: Access should be granted.

---

## Conclusion
By completing this lab, you have practiced:
- Configuring file shares with varying permission levels.
- Testing file share access from different user accounts.
- Managing security groups and applying permission settings in Active Directory.
