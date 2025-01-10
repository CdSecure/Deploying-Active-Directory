<p align="center">
<img src="https://i.imgur.com/xlYwPUf.png" alt="Permissions Photo"/>
</p>

# Deploying-Active-Directory
Installing active directory on the domain controller, and creating users that can join the domain controller.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>Deployment Steps</h2>

  <p>
In this lab, we will install Active Directory on our domain controller, create a domain user account, and join the domain controller using the newly created user. This setup enables us to add and manage any user we create within the domain controller, facilitating centralized user management and authentication.
  </p>
  <p>
    <b>Installing Active Directory on the Domain Controller (DC-1)</b>

We will begin by installing Active Directory on our first virtual machine, designated as DC-1.

### **Steps:**

1. **Access the Domain Controller VM:**
   - Open the Azure portal and navigate to **Virtual Machines**.
   - Select the previously created VM designated as **DC-1**.
   - Click on **Connect** and use **Remote Desktop Protocol (RDP)** to log into the VM with your administrator credentials.

2. **Open Server Manager:**
   - Once logged in, click the **Start** button located at the bottom left corner of the screen.
   - In the Start menu, select **Server Manager** from the list of applications.

3. **Add Roles and Features:**
   - In **Server Manager**, click on **Manage** in the top right corner.
   - From the dropdown menu, select **Add Roles and Features** to launch the wizard.

4. **Navigate Through the Wizard:**
   - **Before You Begin:** Click **Next** to proceed.
   - **Installation Type:** Choose **Role-based or feature-based installation** and click **Next**.
   - **Server Selection:** Ensure that **DC-1** is selected as the destination server and click **Next**.

5. **Select Server Roles:**
   - In the **Server Roles** section, scroll down and check the box for **Active Directory Domain Services**.
   - A prompt will appear to **Add Features** required for AD DS. Click **Add Features**.
   - Click **Next** to continue.

6. **Proceed Through Features:**
   - **Features:** Click **Next** without selecting any additional features.
   - **AD DS:** Review the information provided and click **Next**.

7. **Confirm Installation Selections:**
   - Review the summary of roles and features to be installed.
   - Check the box for **Restart the destination server automatically if required** to allow the server to reboot if necessary.
   - Click **Install** to begin the installation process.

8. **Complete Installation:**
   - The installation will proceed, and once completed, you will be prompted to **Restart** the server.
   - Click **Yes** to initiate the restart.
   - After the server restarts, the installation of Active Directory Domain Services will be finalized.
  </p>
  
  <p>
    <img width="1800" alt="Screenshot 2024-11-14 at 2 29 20 PM" src="https://github.com/user-attachments/assets/e0d62993-c188-481a-940e-295b621022cb">
  </p>
  <p><img width="369" alt="Screenshot 2024-11-14 at 2 31 46 PM" src="https://github.com/user-attachments/assets/f0376d16-8642-46a6-8ca0-8f9195739f51"></p>
  <p>
    <img width="785" alt="Screenshot 2024-11-14 at 2 38 04 PM" src="https://github.com/user-attachments/assets/3ab611fa-0efb-4ce9-a6d7-db516db798cb">
  </p>

**Promoting DC-1 to a Domain Controller**

After installing Active Directory on DC-1, we will promote it to a Domain Controller by creating a new forest with the domain name `mydomain.com`.

### **Steps:**

1. **Access Server Manager:**
   - On the DC-1 virtual machine, open **Server Manager**. You can find it by clicking the **Start** button at the bottom left corner or by searching for it in the Start menu.

2. **Initiate Domain Controller Promotion:**
   - In **Server Manager**, locate the notification flag in the top-right corner.
   - Click the flag, and select **Promote this server to a domain controller** from the dropdown menu.

3. **Configure Deployment Configuration:**
   - In the **Active Directory Domain Services Configuration Wizard** that appears, select **Add a new forest**.
   - Enter `mydomain.com` as the **Root domain name**.
   - Click **Next** to proceed.

4. **Set Domain Controller Options:**
   - In the **Domain Controller Options** section, set the **Directory Services Restore Mode (DSRM) password** to `Password1`.
   - Ensure that the appropriate options are selected based on your requirements.
   - Click **Next** to continue.

5. **Proceed Through the Wizard:**
   - Continue clicking **Next** through the subsequent screens, reviewing each configuration as needed.
   - Accept the default settings unless specific changes are required for your environment.

6. **Install Active Directory:**
   - On the **Prerequisites Check** page, review any warnings or errors. Address them if necessary.
   - Click **Install** to begin the promotion process.

7. **Restart the Server:**
   - After the installation completes, the server will automatically restart to apply the changes.
     
<p>
  <img width="1800" alt="Screenshot 2024-11-14 at 3 03 20 PM" src="https://github.com/user-attachments/assets/3917bcd7-0812-4392-8c85-314313565181">
</p>
<p>
  <img width="350" alt="Screenshot 2024-11-14 at 3 03 45 PM" src="https://github.com/user-attachments/assets/01ddb576-409b-48e0-a9e2-3a3f9f87db71">
</p>
<p>
  <img width="759" alt="Screenshot 2024-11-14 at 3 04 51 PM" src="https://github.com/user-attachments/assets/b08c0862-fafc-465d-926f-5e5740395dc1">
</p>
<p>
  <img width="761" alt="Screenshot 2024-11-14 at 3 12 09 PM" src="https://github.com/user-attachments/assets/55af0bcf-ab50-4eb2-9e33-74ab1b49becd">
</p>
<p>
  <img width="754" alt="Screenshot 2024-11-14 at 3 15 02 PM" src="https://github.com/user-attachments/assets/3cc37fd0-108d-4d52-8d43-bcb035a31796">
</p>

**Logging into the Domain Controller as a Domain User and Creating a Domain Admin Account**

After the domain controller (DC-1) has restarted, follow these steps to log in using a domain user account and create a dedicated domain administrator account.


1. **Log into the Domain Controller as a Domain User:**
   
   - **Initiate RDP Connection:**
     - Open **Remote Desktop Protocol (RDP)** on your local machine.
     - Enter the **public IP address** of DC-1 and connect.
   
   - **Authenticate as a Domain User:**
     - On the login screen, instead of using your local credentials, enter the domain user credentials.
     - Use the format `mydomain.com\labuser` where:
       - `mydomain.com` is your domain name.
       - `labuser` is the domain user account you created earlier.
     - Enter the corresponding **password** for `labuser`.
     - Click **OK** to log in.

2. **Verify Domain User Login:**
   
   - Upon successful login, the **Server Manager** should automatically appear.
   - If **Server Manager** does not launch, ensure you have logged into the correct VM and are using domain credentials.

<img width="437" alt="Screenshot 2024-11-14 at 3 33 44 PM" src="https://github.com/user-attachments/assets/3cc4edbf-e77d-4a2e-ad50-0195f4dfd290">

**Creating Organizational Units and a Domain User in Active Directory**

Now that we are logged into the domain controller, we will create two Organizational Units (OUs): `_ADMINS` and `_EMPLOYEES`. Subsequently, we will create a domain user account within the `_ADMINS` OU.

### **Steps:**

1. **Open Active Directory Users and Computers:**
   - Click the **Start** button located at the bottom left corner of the screen.
   - In the search bar, type **"Active Directory Users and Computers"** and press **Enter** to launch the application.

2. **Create Organizational Units (OUs):**
   - In the **Active Directory Users and Computers** window, locate your domain (`mydomain.com`) in the left pane.
   - Right-click on **mydomain.com**, select **New**, and then choose **Organizational Unit**.
   - In the **Name** field, enter `_ADMINS`.
   - Ensure that the **Protect container from accidental deletion** option is checked.
   - Click **OK** to create the `_ADMINS` OU.
   - Repeat the process to create the `_EMPLOYEES` OU:
     - Right-click on **mydomain.com**, select **New**, and then choose **Organizational Unit**.
     - Enter `_EMPLOYEES` as the **Name**.
     - Click **OK**.

3. **Create a User in the _ADMINS OU:**
   - Navigate to the newly created `_ADMINS` OU by expanding **mydomain.com** and selecting `_ADMINS`.
   - Right-click on the `_ADMINS` OU, select **New**, and then choose **User**.
   - In the **New Object - User** dialog box, fill in the following details:
     - **First name:** Jane
     - **Last name:** Doe
     - **User logon name:** jane.doe
   - Click **Next**.

4. **Set User Password and Options:**
   - Enter a **password** for the user in both the **Password** and **Confirm password** fields.
   - Uncheck the **User must change password at next logon** option.
   - Check the **Password never expires** option.
   - Click **Next**.
   - Review the information and click **Finish** to create the user account.

<img width="1800" alt="Screenshot 2024-11-14 at 4 11 51 PM" src="https://github.com/user-attachments/assets/6fb8e09d-75df-41cc-a2df-565149302431">

<img width="1316" alt="Screenshot 2024-11-14 at 4 47 34 PM" src="https://github.com/user-attachments/assets/7d990a2c-25c3-4ece-a3a8-4994198488cb">

<img width="1314" alt="Screenshot 2024-11-14 at 4 24 13 PM" src="https://github.com/user-attachments/assets/c912adc2-6244-4956-8efb-7503e14d3789">

<img width="433" alt="Screenshot 2024-11-14 at 4 24 42 PM" src="https://github.com/user-attachments/assets/a6ec5cd6-b3da-45b1-8f21-1bfe47fe8551">

<img width="434" alt="Screenshot 2024-11-14 at 4 25 22 PM" src="https://github.com/user-attachments/assets/56b9c519-0df4-4130-baf6-2209aa50e726">

**Promoting a User to Domain Administrator**

To ensure that Jane Doe has administrative privileges within the domain, we will add her account to the **Domain Admins** group. This process involves modifying her user properties in Active Directory.

### **Steps:**

1. **Open Active Directory Users and Computers:**
   - Click the **Start** button at the bottom left corner.
   - Type **"Active Directory Users and Computers"** in the search bar and press **Enter** to launch the application.

2. **Navigate to Jane Doe’s User Account:**
   - In the **Active Directory Users and Computers** window, locate your domain (`mydomain.com`) in the left pane.
   - Expand the domain and navigate to the **_ADMINS** Organizational Unit (OU) where Jane Doe was created.
   - Right-click on **Jane Doe's** user account and select **Properties** from the context menu.

3. **Modify Group Membership:**
   - In the **Jane Doe Properties** window, navigate to the **Member Of** tab.
   - Click the **Add** button to open the **Select Groups** dialog box.

4. **Add to Domain Admins Group:**
   - In the **Select Groups** dialog, type **"Domain Admins"** into the **Enter the object names to select** field.
   - Click **Check Names** to verify the group name. It should underline if recognized correctly.
   - Click **OK** to add **Domain Admins** to Jane Doe’s group memberships.

5. **Apply Changes:**
   - Back in the **Member Of** tab, ensure that **Domain Admins** is now listed among Jane Doe’s groups.
   - Click **Apply**, then **OK** to save the changes and close the properties window.

6. **Verify Administrative Privileges:**
   - Log out of the current session by clicking the **Start** button, selecting your user icon, and choosing **Sign out**.
   - Log back into DC-1 using the domain administrator credentials:
     - **Username:** `mydomain.com\adminuser` (replace `adminuser` with the actual admin username).
     - **Password:** Enter the password you set for the domain admin account.
   - Upon successful login, ensure that **Server Manager** opens automatically, confirming administrative access.
<img width="1800" alt="Screenshot 2024-11-14 at 5 09 07 PM" src="https://github.com/user-attachments/assets/652a0006-94f1-4af5-b86a-3f030c09287c">


<img width="408" alt="Screenshot 2024-11-14 at 5 09 15 PM" src="https://github.com/user-attachments/assets/fdf82b95-4aef-4d08-97d0-4a61b32d5729">

<img width="453" alt="Screenshot 2024-11-14 at 5 09 36 PM" src="https://github.com/user-attachments/assets/a4c922dc-9208-407c-8eea-51a91ae24a02">


**Joining Client-1 to the Domain**

Now that you are logged in as `jane_admin`, we will connect Client-1 to the domain. Follow these steps to successfully join the domain:

### **Steps:**

1. **Access System Settings on Client-1:**
   - **Right-Click Start Menu:**
     - On Client-1, right-click the **Start** button located at the bottom left corner of the screen.
   - **Select System:**
     - From the context menu, click on **System** to open the System settings window.

2. **Initiate PC Renaming Process:**
   - **Click "Rename this PC":**
     - In the System settings window, locate and click on the **"Rename this PC"** option. This will open the Rename PC dialog box.

3. **Change Domain Membership:**
   - **Click Change:**
     - In the Rename PC dialog, click the **Change** button to modify the computer's domain settings.
   - **Enter Domain Information:**
     - In the **Member of** section, select **Domain**.
     - Enter the domain name **`mydomain.com`** in the provided field.
   - **Confirm Changes:**
     - Click **OK** to proceed with joining the domain.

4. **Authenticate with Domain Credentials:**
   - **Enter Domain User Credentials:**
     - A prompt will appear requesting credentials. Enter the domain administrator credentials:
       - **Username:** `mydomain.com\jane_admin`
       - **Password:** [Enter the password for `jane_admin`]
   - **Click OK:**
     - After entering the credentials, click **OK** to authenticate and join the domain.

5. **Complete Domain Join Process:**
   - **Welcome Message:**
     - Upon successful authentication, a window will display a message such as **"Welcome to mydomain.com"** confirming that the PC has joined the domain.
   - **Restart the Computer:**
     - You will be prompted to restart the computer to apply the changes. Click **Restart Now** to reboot Client-1.

6. **Log In with Domain Credentials:**
   - **Select Domain Account:**
     - After the restart, at the login screen, select **Other user**.
   - **Enter Domain Credentials:**
     - Log in using the domain account:
       - **Username:** `mydomain.com\jane_admin`
       - **Password:** [Enter the password for `jane_admin`]
   - **Access Domain Resources:**
     - Upon successful login, you will have access to domain-controlled resources and settings, confirming that Client-1 is now part of the `mydomain.com` domain.
    
<img width="435" alt="Screenshot 2024-11-14 at 5 16 19 PM" src="https://github.com/user-attachments/assets/771105be-4dbe-431b-a097-5dedc915ac2d">

<img width="1198" alt="Screenshot 2024-11-14 at 5 21 09 PM" src="https://github.com/user-attachments/assets/2509810f-df21-4b53-993a-3e54d3054ade">

<img width="734" alt="Screenshot 2024-11-14 at 5 23 16 PM" src="https://github.com/user-attachments/assets/0df56269-ca39-4636-b898-0fa78cdb123f">

<img width="295" alt="Screenshot 2024-11-14 at 5 25 40 PM" src="https://github.com/user-attachments/assets/aeefffcf-f213-4597-b3ea-cc052f448a10">


**Confirming Client-1's Domain Membership and Organizing into an Organizational Unit**

In this step, we will verify that Client-1 is successfully joined to the domain managed by DC-1 and organize its computer account into a dedicated Organizational Unit (OU) for better management.

### **Steps:**

1. **Open Active Directory Users and Computers:**
   
   - On the **DC-1** domain controller, click the **Start** button at the bottom left corner.
   - In the search bar, type **"Active Directory Users and Computers"** and press **Enter** to launch the application.

2. **Navigate to the Computers Container:**
   
   - In the **Active Directory Users and Computers** window, locate and expand your domain (`mydomain.com`) in the left pane.
   - Click on the **Computers** container to view all computer accounts within the domain.

3. **Verify Client-1's Domain Membership:**
   
   - In the **Computers** container, look for **Client-1**. This confirms that Client-1 is successfully joined to the domain.
   - If **Client-1** is not visible, ensure that the client VM was correctly joined to the domain and that it has communicated with the domain controller.

4. **Create a New Organizational Unit (OU) for Clients:**
   
   - Right-click on your domain name (`mydomain.com`) in the left pane.
   - Select **New** > **Organizational Unit** from the context menu.
   - In the **Name** field, enter **_CLIENTS** (ensure the underscore is included for consistent naming conventions).
   - Ensure the **Protect container from accidental deletion** option is checked to prevent accidental removal.
   - Click **OK** to create the **_CLIENTS** OU.

5. **Move Client-1's Computer Account to the _CLIENTS OU:**
   
   - Navigate back to the **Computers** container by clicking on it.
   - Locate **Client-1** in the list of computer accounts.
   - Click and drag **Client-1** into the newly created **_CLIENTS** OU in the left pane.
   - Alternatively, right-click on **Client-1**, select **Move**, choose **_CLIENTS** from the list, and click **OK**.

6. **Confirm the Move:**
   
   - Click on the **_CLIENTS** OU to ensure that **Client-1** now resides within it.
   - This organization helps in managing client machines separately from other computer accounts, enhancing administrative efficiency.

<img width="751" alt="Screenshot 2024-11-14 at 5 31 35 PM" src="https://github.com/user-attachments/assets/d293b5e3-8add-4f17-91d1-115a36326acf">

<img width="724" alt="Screenshot 2024-11-14 at 5 34 23 PM" src="https://github.com/user-attachments/assets/f45b5a14-9d2b-4931-a401-018f563f935e">

**Summary of Network Configuration and Domain Setup**

In this lab, we established a virtual network in Microsoft Azure by creating a resource group and configuring a virtual network with dedicated subnets for a Windows Server domain controller (DC-1) and a Windows 10 client machine. We installed and configured Active Directory on DC-1, promoted it to a domain controller with the domain name `mydomain.com`, and organized users into Organizational Units (_ADMINS and _EMPLOYEES). By joining Client-1 to the domain and verifying network connectivity, we ensured centralized management and seamless communication between the client and the domain controller. Additionally, we created and promoted a domain user to an administrator role. Moving forward, we will create additional user accounts using PowerShell to streamline and automate domain administration.
