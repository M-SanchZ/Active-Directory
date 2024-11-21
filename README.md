![image](https://github.com/user-attachments/assets/fe888fe7-ca6b-455e-b30c-1b77188f1e42)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop


<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)


# **Active Directory Lab Tutorial - Part 1 & Part 2**

In this tutorial, we will walk through the steps for setting up Active Directory, creating domain users, managing permissions, and configuring Remote Desktop access for non-administrative users. This will involve working with **DC-1** (Domain Controller) and **Client-1** virtual machines within an Azure environment.

---

## **Part 1: Set Up Active Directory**

### **1.1 Install Active Directory Domain Services**

1. **Login to DC-1**:  
   Log into the **DC-1** virtual machine using your credentials.

2. **Install Active Directory Domain Services**:  
   - Open **Server Manager**.
   - Click **Add Roles and Features**.
   - Select **Role-based or feature-based installation** and proceed to the **Roles** section.
   - Select **Active Directory Domain Services** and click **Next** to install.
     ![image](https://github.com/user-attachments/assets/807f18c1-2e9c-4958-906c-c4d973d9f6fa)
     ![image](https://github.com/user-attachments/assets/9a431209-1f4a-4ff6-9586-9e399069546c)
     ![image](https://github.com/user-attachments/assets/922111e0-01ce-4d0a-b7d6-4fcb612b5522)
     ![image](https://github.com/user-attachments/assets/33b3007a-184d-467f-ac5c-7a818eddbbc6)
     ![image](https://github.com/user-attachments/assets/3cda9b85-c03a-4c50-a1c4-0da25ffbd6f0)
     ![image](https://github.com/user-attachments/assets/5b100dff-cb56-49ce-b8a8-78383cc32a18)
     ![image](https://github.com/user-attachments/assets/44f4a4e2-37e2-43d2-b4ba-130d90b10074)
     ![image](https://github.com/user-attachments/assets/3de0861d-567a-4291-97e7-18d09b589162)
     ![image](https://github.com/user-attachments/assets/45bae865-c99c-48d1-8057-73287d6e608a)
     ![image](https://github.com/user-attachments/assets/ce6032e7-6c3a-4b2a-8f5c-065d40106352)
     ![image](https://github.com/user-attachments/assets/6d533257-a8eb-4356-a047-aa27f40a2906)












3. **Promote as a Domain Controller**:  
   After installation, click the **promote this server to a domain controller** link in Server Manager.
   - Choose **Add a new forest** and set the **Domain Name** to `mydomain.com` (you can choose a different name but remember it for later).
   - Set up a **Directory Services Restore Mode (DSRM) password**.
   - Complete the wizard and allow the server to **restart**.
     ![image](https://github.com/user-attachments/assets/27c4e54c-5708-46d3-8f7a-9ffaca17a70c)
     ![image](https://github.com/user-attachments/assets/19740026-67c4-4177-9824-0b8a55a6bd5a)
     ![image](https://github.com/user-attachments/assets/a468cf23-58e9-43ed-83dc-3b8b4e562cd8)
     ![image](https://github.com/user-attachments/assets/1eb77852-4471-40bc-8445-0ff087bd4de9)
     ![image](https://github.com/user-attachments/assets/8c84bd16-23dd-4686-9d34-d861fbcb5ef9)
     ![image](https://github.com/user-attachments/assets/4d9509cb-8a7e-47c1-a8d8-53b1838b8f09)
     ![image](https://github.com/user-attachments/assets/d8b1bbc7-cfcf-4456-8409-a32d39681e0c)
     ![image](https://github.com/user-attachments/assets/002c1ace-1786-4f55-9c58-6f2943d16bc7)
     ![image](https://github.com/user-attachments/assets/c4fb87f9-03a7-4742-bf37-34f4c4b832a0)
     ![image](https://github.com/user-attachments/assets/77a9d9bc-fc0c-422c-afb2-23de190e4f63)
     ![image](https://github.com/user-attachments/assets/1181020e-4b44-4ae9-b904-f643c5bf9645)
     ![image](https://github.com/user-attachments/assets/bacf4da6-839b-4f55-8791-4672b973140e)
     ![image](https://github.com/user-attachments/assets/526e8b8a-0850-4426-9ffd-7a3cf01e16ba)













     

4. **Login to DC-1 as labuser**:  
   After the server restarts, log back into **DC-1** using the **labuser** credentials (e.g., `mydomain.com\labuser`).
   ![image](https://github.com/user-attachments/assets/26b641bf-ddd8-43a8-8343-b88b76769b95)


---

### **1.2 Create a Domain Admin User**

1. **Open Active Directory Users and Computers (ADUC)**:  
   - On **DC-1**, open **Active Directory Users and Computers**.
   - Right-click the **Users** folder and select **New Organizational Unit (OU)**.
   - Create an OU named `_EMPLOYEES` and click **OK**.
     ![image](https://github.com/user-attachments/assets/9b679985-75e4-4dd1-a8fb-fade008dd39a)

     ![image](https://github.com/user-attachments/assets/fd8412b8-97a9-47a4-989f-fa37eeca46bb)
     ![image](https://github.com/user-attachments/assets/da8cb9da-1d18-4d01-80d0-e516a3212728)
     ![image](https://github.com/user-attachments/assets/cdf5e28d-cd57-4cc7-88e6-0649746e12ff)
     ![image](https://github.com/user-attachments/assets/6bc9c343-578f-4615-9625-0e7a26b2b981)
     ![image](https://github.com/user-attachments/assets/f9bd28f0-419a-4e4c-af7a-6199f1ad9e4e)
     ![image](https://github.com/user-attachments/assets/fabd9c9a-ad65-45a9-930d-90f1bff590b7)







     

2. **Create a New Organizational Unit (OU) for Admins**:  
   - Right-click on the root domain and select **New Organizational Unit**.
   - Create an OU named `_ADMINS` and click **OK**.
     ![image](https://github.com/user-attachments/assets/f4f212e9-8973-4c02-8f59-15ce1ce88f4c)
     ![image](https://github.com/user-attachments/assets/6b2b5094-9af4-46ee-98de-5c2060ecaa71)
     ![image](https://github.com/user-attachments/assets/bdedf304-1a1a-485d-9fa6-c3aa1e38cfab)




3. **Create a New Employee Account**:  
   - Right-click on the `_EMPLOYEES` OU and select **New > User**.
   - Enter the following details for the new employee:
     - **Full Name**: Jane Doe
     - **Username**: `jane_admin`
     - **Password**: `Cyberlab123!`
     - Ensure the option **User must change password at next logon** is unchecked. This is not Ok to do, but for the sake of this lab we will uncheck t         this box
       ![image](https://github.com/user-attachments/assets/1f4ff91b-1819-4f3d-93f1-a1399aac8605)
       ![image](https://github.com/user-attachments/assets/c2cdf91a-fcdb-4934-b0c5-2f04bd344b44)
       ![image](https://github.com/user-attachments/assets/01b6041c-0cba-47b7-a6d3-848d8519a476)
       ![image](https://github.com/user-attachments/assets/4e49e821-3445-43ce-b6c7-7b2bfb2f166e)




       

4. **Add `jane_admin` to the Domain Admins Group**:  
   - Right-click the **Domain Admins** group and select **Add to Group**.
   - Add `jane_admin` to the group.
     ![image](https://github.com/user-attachments/assets/4c764f6e-7fbb-4b2b-813e-7937bce051ee)
     ![image](https://github.com/user-attachments/assets/5e9f153a-ec40-47e2-a000-639b620878b8)
     ![image](https://github.com/user-attachments/assets/c31a3bc7-38d8-4075-8d81-6e977cbf4624)
     ![image](https://github.com/user-attachments/assets/f322f1f9-9958-43d8-9cd2-44955e31f3f8)
     ![image](https://github.com/user-attachments/assets/08dbb8c3-a69f-4156-8171-f151493cc30c)
     ![image](https://github.com/user-attachments/assets/84dbb532-fd8a-4f23-b463-94c7a6b2e78d)
     ![image](https://github.com/user-attachments/assets/8c287ca6-9f44-4e5a-8708-061b712f332d)
     ![image](https://github.com/user-attachments/assets/6866bc37-81d0-4ffd-89f3-b25decc1d463)
     ![image](https://github.com/user-attachments/assets/2cdf8ea3-7ce7-47f6-aaba-a9e0f97f6c38)






5. **Log Out and Log In as `jane_admin`**:  
   - Log out from **DC-1** and log back in as `mydomain.com\jane_admin` (use the password `Cyberlab123!`).
     ![image](https://github.com/user-attachments/assets/3800e0ec-dc92-4331-ac80-fce447668560)


---

### **1.3 Join Client-1 to the Domain**

1. **Set DNS Settings for Client-1**:  
   In the Azure portal, ensure **Client-1's** DNS settings are configured to the **Private IP** address of the Domain Controller (DC-1). If you did this already, just double check if it is still configured to DC-1's Private IP address.
   ![image](https://github.com/user-attachments/assets/d5012274-b32e-4b58-a6c3-684b8d2fcce5)
   ![image](https://github.com/user-attachments/assets/060e0fe4-376f-4124-bb8b-a866ab5f6b38)
   ![image](https://github.com/user-attachments/assets/926eadf4-e797-4799-a964-e9c68de7225b)
   ![image](https://github.com/user-attachments/assets/5f1dd867-3288-4d1f-9efc-6bc347dc7c2c)


   

3. **Restart Client-1**:  
   Restart **Client-1** to apply the changes (already done).

4. **Login to Client-1 and Join the Domain**:  
   - Log into **Client-1** as the original local admin (`labuser`).
   - Open **System Properties** > **Computer Name** tab.
   - Click **Change** and set the computer to join the **mydomain.com** domain.
   - After the computer restarts, log in as `mydomain.com\labuser` to verify the domain join.

5. **Verify Client-1 in ADUC**:  
   - Log back into **DC-1** as `jane_admin` and open **Active Directory Users and Computers**.
   - Verify that **Client-1** shows up in the domain.

6. **Create an OU for Clients**:  
   - Right-click on the root domain and select **New > Organizational Unit**.
   - Name the new OU `_CLIENTS` and click **OK**.
   - Drag **Client-1** into the newly created `_CLIENTS` OU.

7. **Shutdown VMs** (Optional):  
   - If you're done for the day and want to save resources, you can stop the VMs in the Azure portal. Do not delete the VMs as they will be used in upcoming labs.

---

## **Part 2: Remote Desktop and User Management**

### **2.1 Enable Remote Desktop for Non-Admin Users on Client-1**

1. **Login to Client-1 as `jane_admin`**:  
   Log into **Client-1** as `mydomain.com\jane_admin`.

2. **Configure Remote Desktop Access**:
   - Open **System Properties** (right-click **This PC** > **Properties**).
   - Click on **Remote settings** on the left sidebar.
   - Under **Remote Desktop**, select **Allow remote connections to this computer**.
   - In the **Select Users** window, add **Domain Users** to grant access to Remote Desktop.

3. **Log In as a Domain User**:  
   You can now log into **Client-1** as a normal domain user. For example, you can log in with any **_EMPLOYEES** account and confirm that Remote Desktop access works.

---

### **2.2 Create Multiple Users and Test Login to Client-1**

1. **Login to DC-1 as `jane_admin`**:  
   Log into **DC-1** as `mydomain.com\jane_admin`.

2. **Create User Accounts Using PowerShell**:
   - Open **PowerShell ISE** as an administrator.
     [Paste the following script to create multiple user accounts](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

---

### **2.2 Test Logging into Client-1**

1. **Verify User Creation in ADUC**:
   - Open **Active Directory Users and Computers** (ADUC) on **DC-1**.
   - Confirm that the newly created users appear in the **_EMPLOYEES** Organizational Unit (OU).

2. **Test Logging into Client-1**:
   - Attempt to log into **Client-1** using one of the newly created user accounts. For example, use `mydomain.com\john_smith`.
   - Use the password set in the script (e.g., `Cyberlab123!`) to log in.

---

### **2.3 Finalizing the Lab**

1. **Stop VMs for Resource Saving**:
   - After completing the lab, do **not delete the VMs** in Azure.
   - Instead, go to the **Azure portal** and **stop** both **DC-1** and **Client-1** to save resources.

---

## **Conclusion**

In this tutorial, you have:
- Installed **Active Directory Domain Services** and promoted your server as a **Domain Controller**.
- Created a **domain admin user** and organized domain users within **Organizational Units (OUs)**.
- Joined **Client-1** to your domain and configured **Remote Desktop access** for non-administrative users.
- Created multiple **domain user accounts** using PowerShell and logged into **Client-1** as one of the new users.

---

**End of Lab**
