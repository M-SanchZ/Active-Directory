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

3. **Promote as a Domain Controller**:  
   After installation, click the **promote this server to a domain controller** link in Server Manager.
   - Choose **Add a new forest** and set the **Domain Name** to `mydomain.com` (you can choose a different name but remember it for later).
   - Set up a **Directory Services Restore Mode (DSRM) password**.
   - Complete the wizard and allow the server to **restart**.

4. **Login to DC-1 as labuser**:  
   After the server restarts, log back into **DC-1** using the **labuser** credentials (e.g., `mydomain.com\labuser`).

---

### **1.2 Create a Domain Admin User**

1. **Open Active Directory Users and Computers (ADUC)**:  
   - On **DC-1**, open **Active Directory Users and Computers**.
   - Right-click the **Users** folder and select **New Organizational Unit (OU)**.
   - Create an OU named `_EMPLOYEES` and click **OK**.

2. **Create a New Organizational Unit (OU) for Admins**:  
   - Right-click on the root domain and select **New Organizational Unit**.
   - Create an OU named `_ADMINS` and click **OK**.

3. **Create a New Employee Account**:  
   - Right-click on the `_EMPLOYEES` OU and select **New > User**.
   - Enter the following details for the new employee:
     - **Full Name**: Jane Doe
     - **Username**: `jane_admin`
     - **Password**: `Cyberlab123!`
     - Ensure the option **User must change password at next logon** is unchecked.

4. **Add `jane_admin` to the Domain Admins Group**:  
   - Right-click the **Domain Admins** group and select **Add to Group**.
   - Add `jane_admin` to the group.

5. **Log Out and Log In as `jane_admin`**:  
   - Log out from **DC-1** and log back in as `mydomain.com\jane_admin` (use the password `Cyberlab123!`).

---

### **1.3 Join Client-1 to the Domain**

1. **Set DNS Settings for Client-1**:  
   In the Azure portal, ensure **Client-1's** DNS settings are configured to the **Private IP** address of the Domain Controller (DC-1).

2. **Restart Client-1**:  
   Restart **Client-1** to apply the changes (already done).

3. **Login to Client-1 and Join the Domain**:  
   - Log into **Client-1** as the original local admin (`labuser`).
   - Open **System Properties** > **Computer Name** tab.
   - Click **Change** and set the computer to join the **mydomain.com** domain.
   - After the computer restarts, log in as `mydomain.com\labuser` to verify the domain join.

4. **Verify Client-1 in ADUC**:  
   - Log back into **DC-1** as `jane_admin` and open **Active Directory Users and Computers**.
   - Verify that **Client-1** shows up in the domain.

5. **Create an OU for Clients**:  
   - Right-click on the root domain and select **New > Organizational Unit**.
   - Name the new OU `_CLIENTS` and click **OK**.
   - Drag **Client-1** into the newly created `_CLIENTS` OU.

6. **Shutdown VMs** (Optional):  
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
   - Paste the following script to create multiple user accounts:

```powershellRun the script to create the user accounts and add them to the _EMPLOYEES OU.

 # ----- Edit these Variables for your own Use Case ----- #
$PASSWORD_FOR_USERS   = "Password1"
$NUMBER_OF_ACCOUNTS_TO_CREATE = 10000
# ------------------------------------------------------ #

Function generate-random-name() {
    $consonants = @('b','c','d','f','g','h','j','k','l','m','n','p','q','r','s','t','v','w','x','z')
    $vowels = @('a','e','i','o','u','y')
    $nameLength = Get-Random -Minimum 3 -Maximum 7
    $count = 0
    $name = ""

    while ($count -lt $nameLength) {
        if ($($count % 2) -eq 0) {
            $name += $consonants[$(Get-Random -Minimum 0 -Maximum $($consonants.Count - 1))]
        }
        else {
            $name += $vowels[$(Get-Random -Minimum 0 -Maximum $($vowels.Count - 1))]
        }
        $count++
    }

    return $name

}

$count = 1
while ($count -lt $NUMBER_OF_ACCOUNTS_TO_CREATE) {
    $fisrtName = generate-random-name
    $lastName = generate-random-name
    $username = $fisrtName + '.' + $lastName
    $password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force

    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $firstName `
               -Surname $lastName `
               -DisplayName $username `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=_EMPLOYEES,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true
    $count++
}

