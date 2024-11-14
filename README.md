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
    **Installing Active Directory on the Domain Controller (DC-1)**

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



<img width="1315" alt="Screenshot 2024-11-14 at 4 15 00 PM" src="https://github.com/user-attachments/assets/527b5c7c-f83f-4fa7-b6fd-9c6c980c9aa4">




<img width="1800" alt="Screenshot 2024-11-14 at 4 11 51 PM" src="https://github.com/user-attachments/assets/6fb8e09d-75df-41cc-a2df-565149302431">

