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
[**2.2 Set DNS for Client-1**](https://github.com/M-SanchZ/Setup-Domain-Controller-in-Azure)

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
     ![image](https://github.com/user-attachments/assets/a8804b0b-73b0-4552-a9e1-356a4a3419a3)
     ![image](https://github.com/user-attachments/assets/e72ed12e-720e-4b48-aa77-16f9b24c640e)
     ![image](https://github.com/user-attachments/assets/110d84c6-9649-4aba-bcb9-10c9be15dc42)
     ![image](https://github.com/user-attachments/assets/f2054a8b-b1e7-45df-a64c-4be8af227d01)
     ![image](https://github.com/user-attachments/assets/de331239-e3d9-4471-bdff-b3ab034df3cb)
     ![image](https://github.com/user-attachments/assets/e6beffaf-642d-48fd-b4ed-90f5b37e7448)
     ![image](https://github.com/user-attachments/assets/7ba75b48-33aa-4ea7-9c89-8b3226b02ccf)
     ![image](https://github.com/user-attachments/assets/f5decf09-a50b-4fa1-a1a6-d04797b80e72)
     ![image](https://github.com/user-attachments/assets/77279afb-88cc-42f9-83a8-111e2c387a53)
     ![image](https://github.com/user-attachments/assets/09ffafce-1d2f-41d9-8825-47aedb1b0da5)

   - mydomain.com is the only domain that could be used, anything other than the domain you've created      will not allow you to add a member to.
     ![image](https://github.com/user-attachments/assets/ead2a806-96ac-4ba4-a3ed-24baedf6a264)



     
     

5. **Verify Client-1 in ADUC**:  
   - Log back into **DC-1** as `jane_admin` and open **Active Directory Users and Computers**.
   - Verify that **Client-1** shows up in the domain.
     ![image](https://github.com/user-attachments/assets/504c536d-734c-46f0-b0ce-e25572195118)
     ![image](https://github.com/user-attachments/assets/41706659-a0c6-40f7-803e-1512b7cde8fd)
     ![image](https://github.com/user-attachments/assets/7f018293-1c60-48fa-84a7-f83e03319ff2)
     ![image](https://github.com/user-attachments/assets/a51d1211-71e6-41cf-86f6-4263bb256657)
     ![image](https://github.com/user-attachments/assets/82431367-8496-4826-bc0a-0ceae59e69c1)
     ![image](https://github.com/user-attachments/assets/d4236896-f180-4de7-a5aa-acd0aa0459b3)
     ![image](https://github.com/user-attachments/assets/9222dc70-df69-4d37-ab4f-eac013d6abbb)
     ![image](https://github.com/user-attachments/assets/7f197727-eff7-4e64-a732-06d7ba5e5c8a)
     ![image](https://github.com/user-attachments/assets/68039373-a870-4537-94a4-5be4a8da6c4f)
     ![image](https://github.com/user-attachments/assets/695d6381-5a09-4ca1-87f7-ce1389aeae60)
     ![image](https://github.com/user-attachments/assets/8283f1f4-9e69-410e-a131-d887972c3941)





6. **Create an OU for Clients**:  
   - Right-click on the mydomain and select **New > Organizational Unit**.
   - Name the new OU `_CLIENTS` and click **OK**.
   - Drag **Client-1** into the newly created `_CLIENTS` OU.
     ![image](https://github.com/user-attachments/assets/38f5f531-8606-40d7-a9d9-30d8163e7309)


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
     ![image](https://github.com/user-attachments/assets/a359cca1-43b1-42ce-8618-63d44c452850)
     ![image](https://github.com/user-attachments/assets/49d8c9d4-6208-4301-9246-e5a5663d219b)
     ![image](https://github.com/user-attachments/assets/e99c25b9-35fe-470d-adcd-cf19a3ec1105)
     ![image](https://github.com/user-attachments/assets/b9a4177a-65cb-41dd-b31f-c6753221d6c2)
     ![image](https://github.com/user-attachments/assets/da93cd65-ca97-4746-b111-be161800f2d2)
     ![image](https://github.com/user-attachments/assets/2d62f623-8330-49b5-8043-ed762c0a801b)
     ![image](https://github.com/user-attachments/assets/6e9332df-7766-42c2-be08-af123d4abc00)
     ![image](https://github.com/user-attachments/assets/d7a287f3-29ad-46bf-8266-c85bc9293663)
     ![image](https://github.com/user-attachments/assets/91c58390-b060-4efc-b82c-330773b696ca)
     ![image](https://github.com/user-attachments/assets/42d3906e-4fd9-4b0a-b519-a37be2a927f5)
     ![image](https://github.com/user-attachments/assets/b87e993f-4e3b-4e1f-b50c-6f91843c3255)











     

3. <p style="color: yellow;">Log In as a Domain User:  
   You can now log into <strong>Client-1</strong> as a normal domain user. For example, you can log in with any <strong>_EMPLOYEES</strong> account and confirm that Remote Desktop access works.</p>


---

### **2.2 Create Multiple Users and Test Login to Client-1**

1. **Login to DC-1 as `jane_admin`**:  
   Log into **DC-1** as `mydomain.com\jane_admin`.

2. **Create User Accounts Using PowerShell**:
   - Open **PowerShell ISE** as an administrator.
   - Create New script
   - Save in Desktop: create-users
   - input script 
     [Paste the following script to create multiple user accounts](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

     ![image](https://github.com/user-attachments/assets/4374bcb3-9a16-46fe-ab5b-67b0e18e753a)
     ![image](https://github.com/user-attachments/assets/6b4b38e0-46f4-484c-841f-1b18729587bd)
     ![image](https://github.com/user-attachments/assets/19565926-077b-4b16-a2d9-f31283fe1142)
     ![image](https://github.com/user-attachments/assets/f09dfa5d-4662-44be-a638-c7ee7e85ab4f)





---

### **2.2 Test Logging into Client-1**

1. **Verify User Creation in ADUC**:
   - Open **Active Directory Users and Computers** (ADUC) on **DC-1**.
   - Confirm that the newly created users appear in the **_EMPLOYEES** Organizational Unit (OU).
     ![image](https://github.com/user-attachments/assets/90a0a105-8ec5-4464-b08f-0be60f0f6844)
     ![image](https://github.com/user-attachments/assets/b4efefe5-5feb-410f-9da8-c487ee32210a)



2. **Test Logging into Client-1**:
   - Attempt to log into **Client-1** using one of the newly created user accounts. For example, use `mydomain.com\cik.fif`.
   - Use the password set in the script (e.g., `Password1`) to log in.
   - We can open command Prompt and see that we have a local user logged in.
   - We can also open the User files and see that we are signed in as a User as well as see the admin name
   - We do not have ADMIN access because we are a logged in as a client 
     
     ![image](https://github.com/user-attachments/assets/f6564f0b-4992-49b2-b606-1a45a9c0ebba)
     ![image](https://github.com/user-attachments/assets/0ca49578-973f-48c1-b9c8-61a4564c0da5)
     ![image](https://github.com/user-attachments/assets/d3e10074-c9d9-4b99-963f-adc68a1283ba)
     ![image](https://github.com/user-attachments/assets/f4269747-1b9d-4694-b04f-ed9ab2e69c81)
     ![image](https://github.com/user-attachments/assets/6f0fa8c9-36ec-459e-8855-4cd9eb093af2)






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
