<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial aims to provide step-by-step guidance for beginners in order to install the open-source help desk ticketing system, osTicket. The tutorial is structured to be exceptionally straightforward, ensuring that anyone, regardless of their technical expertise, can easily follow along..<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop Connection
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b>

<h2>List of Prerequisites</h2>

- Active Microsoft Azure subscription
- Stable internet connection

<h2>Installation Steps</h2>

<p>
<b>1.	Create a resource group.</b>

In the Microsoft Azure platform, access "Resource groups" using the search bar and choose "Create." This resource group will serve as the container for our virtual machine where OsTicket will run.

You have the flexibility to name this resource group as you wish, but for clarity, I suggest selecting a name that's easy to identify, especially if you have multiple resource groups. In my case, I'll name it "OsTicket-RG."

Within the resource details, pick the region that aligns with your requirements. I'll be opting for "(Asia Pacific) Australia East."

Next, select "Review and create" followed by "Create."
</p>

<p>
<img src="https://i.imgur.com/ZuXMDpY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>2.	Create a Virtual Machine.</b>

Within Microsoft Azure, utilize the search bar to search "virtual machines," then  select "Create -> Azure virtual machine."

In the "Subscription -> Resource group" section, choose the recently established resource group that we created.

Assign a name to the virtual machine. While the virtual machine can have any name, I advise selecting a name that allows for easy identification. In my case, I'm naming it "OsTicket-VM."

Choose the appropriate region.

In the "Image" section,  select "Windows 10 Pro, Version 21H2 – x64 Gen2."

Under "Size," select "Standard_E2s_v3 – 2 vcpus, 16GiB memory."

Set up a username and password. I'm using "Labuser" and "Password1234."

In the "Licensing" section tick the box “I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights.”

Proceed by selecting "Review and create -> create."

Select “Review and create -> create.”
</p>

<p>
<img src="https://i.imgur.com/c5EIuGS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />


<p>
<b>3.	Connect to the virtual machine via remote desktop connection.</b>

Launch the Remote Desktop Connection application on your personal computer.

Within Microsoft Azure, find the virtual machine that was recently created and copy its Public IP address.

Paste this Public IP address into the Remote Desktop Connection tool and click "Connect."

Select the "Different user" option and provide the login credentials we established during the virtual machine setup, which are "Labuser" and "Password1234."
</p>

<p>
<img src="https://i.imgur.com/JKt4qu9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>4.	Install OsTicket prerequisites.</b>

Once you're inside your virtual machine, launch a web browser and paste the following link into the address bar:

https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6

Next, we'll enable IIS in Windows along with CGI. To accomplish this, access "Control Panel -> Programs -> Turn Windows Features On or Off." Check the box labeled "Internet Information Services" and then expand this option. Within it, expand "World Wide Web Services," and further, expand "Application Development Features." Check the box labeled "CGI" and click OK. Wait for the changes to take effect.

Now, from the "installation files" link we previously opened, download and install the following:

PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)
Rewrite Module (rewrite_amd64_en-US.msi)
Next, we'll create the directory C:\PHP. To do this, open "File Explorer -> This PC -> Windows (C:)." Create a new folder and name it "PHP."

Subsequently, from the Installation Files, download "PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip)." This will download as a compressed (zipped) file. After downloading, extract the contents into C:\PHP.

Also, from the Installation Files, download and install "VC_redist.x86.exe."

Furthermore, from the Installation Files, download "MySQL 5.5.62 (mysql-5.5.62-win32.msi)." <br>
When installing MySQL, choose "Typical" under "Setup Type." <br> 
Under "Server Instance Configuration," select "Standard Configuration." <br>
Use "Password1" for the root password, and finally, click "Execute."
</p>

<p>
<img src="https://i.imgur.com/OM599pC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>5.	Reload IIS</b>


Click the "Start" button, and in the search bar, type "IIS." Right-click and choose to run it as an administrator.

Double-click on "PHP Manager." Under "PHP Setup," choose "Register new PHP version," and then click the three dots on the right side of the search bar. In the File Explorer, navigate to "This PC -> Windows (C:) -> PHP," and select "php.cgi." Click "OK."

On the left side of IIS Services, select the server's name, which is "OsTicket-VM." Then, on the right side, under "Actions -> Manage server," select "Restart server."

Finally, close IIS Services.
</p>

<p>
<img src="https://i.imgur.com/ZX7m9le.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>6.	Install OsTicket</b>

Download the "OsTicket v1.15.8" from the installation files.

Open the zip file we just downloaded, which is named "OsTicket v1.15.8," using File Explorer. Simultaneously, open another File Explorer window and navigate to "This PC -> Windows (C:) -> inetpub -> wwwroot." Then, simply drag the folder labeled "upload" from the "OsTicket v1.15.8" zip file into the "wwwroot" directory. Rename the "upload" folder to "osTicket," ensuring it is spelled exactly as I have written, without any spaces.
</p>

<p>
<img src="https://i.imgur.com/R6JWlXn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>

Revisit the IIS services and perform the server restart, just as we did earlier.

In the IIS Services window, expand "OsTicket-VM -> Sites -> Default Web Site" on the left-hand side, and then select "osTicket." On the right-hand side, choose "Browse *:80 (http)." This action will launch the osTicket installer in a web page.
</p>

<p>
<img src="https://i.imgur.com/hNqvgIZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Navigate to "OsTicket-VM -> Sites -> Default Web Site -> osTicket" within IIS, and double-click "PHP Manager." Afterward, click on "Enable or Disable an Extension."

Enable the following extensions:

php_imap.dll
php_intl.dll
php_opcache.dll
Refresh the OsTicket site in your browser to see the changes take effect.

In File Explorer, go to "This PC -> Windows (C:) -> inetpub -> wwwroot -> osTicket -> include" and locate the file named "ost-sampleconfig.php." Rename this file to "ost-config.php."
</p>

<p>
<img src="https://i.imgur.com/HayNy5A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Right-click on "ost-config.php" and choose "Properties." Then, click on "Security," followed by "Advanced."

Select "Disable inheritance," and opt to "Remove all inherited permissions from this object."

Inside the "Advanced" settings, choose "Add," and then click "Select a principle." In the search box, type "everyone," and click "Check names." Afterward, click "OK."

Tick the checkbox labeled "Full control," click "OK," and then press "Apply" followed by "OK."
</p>

<p>
<img src="https://i.imgur.com/OGQptoF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>7.	Setup OsTicket in the browser.</b>

Go back to the browser window with OsTicket open and click on "Continue."

In the System Settings, provide a name for your helpdesk. Once again, this can be anything you prefer. I'll name mine "ExampleHelpDesk." In the "Default Email" field, enter an email address. I will use "Johndoe@helpdesk.com."

Next, set up your admin user. Ensure that you remember these login credentials because you will use them to access OsTicket as the admin. I recoomend writing these credentials down. For this purpose, I will use
First name: John
Last name: Doe
Email address: johndoe@outlook.com
Username: johndoe
Password: Password1
</p>

<p>
<img src="https://i.imgur.com/YTIhX8J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Next, download "HeidiSQL" from the installation files. After installing HeidiSQL, open the application and choose "New."

On the right-hand side, the "User" field should automatically be filled with "Root." Under "Password," enter the password that was created during the MySQL setup, in this case, we used "Password1." Then, click "Open."

In HeidiSQL's left-hand panel, right-click on "Unnamed" and select "Create new -> Database." Name the database "osTicket."

Return to the web page with the OsTicket installer open. Under “Database settings -> MySQL database” Type “osTicket”. Under “MySQL Username” type “Root”. Under “MySQL Password” type the password we created, being “Password1”. Finally select “Install now”.
</p>

<p>
<img src="https://i.imgur.com/dJ2SqqU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>8.	Cleanup</b>

Before we can begin using OsTicket, we need to perform some cleanup steps.

Using File Explorer, navigate to "This PC -> Windows (C:) -> inetpub -> wwwroot -> osTicket" and delete the folder labeled "Setup."

Then, go to "This PC -> Windows (C:) -> inetpub -> wwwroot -> osTicket -> include" and locate the file named "ost-config.php." Right-click on "ost-config.php," select "Properties," go to the "Security" tab, and click on "Advanced." In the "Advanced Security Settings" window, select "Everyone," click "Edit," and ensure that only the "Read" and "Read and execute" checkboxes are selected. Click "OK," "Apply," and then "OK."

Congratulations! You have successfully installed OsTicket. In the next tutorial, we will cover how to configure OsTicket post-installation.
</p>

<br />
