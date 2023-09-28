<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This is a beginner friendly tutorial to help you install the open-source help desk ticketing system osTicket. This tutorial is designed to be as simple as possible so that anybody should be able to follow along easily.<br />


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

Within Microsoft Azure, navigate to “Resource groups” via the search bar and select “Create.” Inside this resource group is where we will store our virtual machine that will run OsTicket.

This resource group can be named anything, however I recommend naming it something that will be easy to recognize if you have multiple resource groups. I will use the name “OsTicket-RG.”

Under resource details, select the region that is relevant to you. I am using “(Asia Pacific) Australia East”.

Select “Review and create” then “Create.”
</p>

<p>
<img src="https://i.imgur.com/ZuXMDpY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>2.	Create a Virtual Machine.</b>

Within Microsoft Azure, navigate to “virtual machines” via the search bar and select “Create -> Azure virtual machine.”

Under “Subscription -> Resource group” Select the resource group we just created.

Name the virtual machine. Again, the virtual machine can be named anything, however I recommend naming it something that makes it easily identifiable. I will be naming it “OsTicket-VM.”

Select your relevant region.

Under “image” select “Windows 10 Pro, Version 21H2 – x64 Gen2.”

Under “Size” select “Standard_E2s_v3 – 2 vcpus, 16GiB memory.”

Create a username and password. I will be using “Labuser” and “Password1234.”

Under “Licensing” tick the box “I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights.”

Select “Review and create -> create.”
</p>

<p>
<img src="https://i.imgur.com/c5EIuGS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />


<p>
<b>3.	Connect to the virtual machine via remote desktop connection.</b>

Open remote desktop connection on your PC.

In Microsoft Azure, navigate to the virtual machine we just created and copy the Public IP address.

Paste the public IP address into remote desktop connection, then press “connect.”

Select “Different user” and input the credentials we used when creating the virtual machine being, “Labuser” and “Password1234.”
</p>

<p>
<img src="https://i.imgur.com/JKt4qu9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>4.	Install OsTicket prerequisites.</b>

Once inside your virtual machine, open a web browser and paste the link below into the search bar.

https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6

Next, we will enable IIS in Windows with CGI. To do this open “Control panel -> Programs -> Turn windows features on or off.” Tick the box called “Internet information services” and then expand that box. Within this, expand “World wide web services.” Within this, expand “Application development features” and tick the box labelled “CGI.” Press OK and wait for changes to apply.

From the link we opened before named “installation files” download and install:

PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

Rewrite Module (rewrite_amd64_en-US.msi)

Next, we will Create the directory C:\PHP. To do this open “File explorer -> This PC -> Windows (C:)” Create a new folder and name it “PHP”.

Next, from the Installation Files, download “PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip)” This will download as a “Compressed (Zipped) file” once downloaded unzip the contents into C:\PHP.

Next, from the Installation Files, download and install “VC_redist.x86.exe.”

Next, from the Installation Files, download “MySQL 5.5.62 (mysql-5.5.62-win32.msi)” When installing MySQL, under “Setup type” select “Typical.” Under “Server instance configuration” Select “Standard configuration.” For the root password I will use “Password1”. Finally, press execute.
</p>

<p>
<img src="https://i.imgur.com/OM599pC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>5.	Reload IIS</b>

Press start, search for “IIS” and right click to run as an administrator.

Double click on “PHP Manager.” Under “PHP Setup” select “Register new PHP version” and then select the three dots on the right hand side of the search bar. Within file explorer, navigate to “This PC -> Windows (C:) -> PHP and select “php.cgi” and press okay.

On the left hand side of IIS Services select the name of the server being “OsTicket-VM” and select “Restart server” on the right hand side under “Actions -> Manager server.”

Close IIS Services
</p>

<p>
<img src="https://i.imgur.com/ZX7m9le.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>6.	Install OsTicket</b>

From the installation files download “OsTicket v1.15.8”

In file explorer open the zip file we just downloaded called “OsTicket v1.15.8”. Open another file explorer window and navigate to “This PC -> Windows (C:) -> inetpub -> wwwroot” and then drag the folder labelled “upload” from the “OsTicket v1.15.8” zip file to the “wwwroot” folder. Rename the “upload” folder to “osTicket”. Ensure that it is spelled the same as I have written with no spaces.
</p>

<p>
<img src="https://i.imgur.com/R6JWlXn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Re-open IIS services and restart the server as we did previously.

On the left-hand side of IIS Services, expand “OsTicket-VM -> Sites -> Defualt web site” and select osTicket. On the right hand side select “Browse *:80 (http)” this will open the osTicket installer in a web page.
</p>

<p>
<img src="https://i.imgur.com/hNqvgIZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Within “OsTicket-VM -> Sites -> Defualt web site -> osTicket” double click “PHP Manager” then click “enable or disable an extension” 

Enable:
  
php_imap.dll
  
php_intl.dll
  
php_opcache.dll

Refresh the OsTicket site in your browse to observe changes.

In file explorer navigate to “This PC -> Windows (C:) -> inetpub -> wwwroot -> osTicket -> include” and find the file named “ost-sampleconfig.php” rename this file to “ost-config.php”
</p>

<p>
<img src="https://i.imgur.com/HayNy5A.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
Right-click “ost-config.php” and select “properties” select “Security” select “Advanced” select “Disable inheritance” select “Remove all inherited permissions from this object”

Within “Advanced” select “Add” click “Select a principle” inside the search box type “everyone” press “Check names” press OK. Tick the box titled “Full control” press OK. Press “Apply” press “Okay”.
</p>

<p>
<img src="https://i.imgur.com/OGQptoF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>7.	Setup OsTicket in the browser.</b>

Return to your browser window that has OsTicket open. Press “Continue”

Under System settings give your helpdesk a name, once again this can be anything, I will name mine “ExampleHelpDesk” Under default email write an email address, I will use “Johndoe@helpdesk.com”

Next you will setup your admin user. You will want to remember these credentials, as you will use them to log in to OsTicket as the admin, I recommend writing the credentials down. For this I will use

First name: John
Last name: Doe
Email address: johndoe@outlook.com
Username: johndoe
Password: Password1
</p>

<p>
<img src="https://i.imgur.com/YTIhX8J.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

Next, from the installation files download “HeidiSQL”. Once HeidiSQL is installed open the application, select “New”. On the right-hand side “User” should be auto filled with “Root”. Under “Password” enter the password that we created when setting up MySQL, in this case we used “Password1”. Select “Open”.

On the left hand side of HeidiSQL right click on “Unnamed” and select “Create new -> Database”. Name the database “osTicket”

Return to the web page with the OsTicket installer open. Under “Database settings -> MySQL database” Type “osTicket”. Under “MySQL Username” type “Root”. Under “MySQL Password” type the password we created, being “Password1”. Finally select “Install now”.
</p>

<p>
<img src="https://i.imgur.com/dJ2SqqU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<p>
<b>8.	Cleanup</b>

Before we can use OsTicket we must cleanup some files. 

Using file explorer, navigate to “This PC -> Windows (C:) -> inetpub -> wwwroot -> osTicket” and delete the folder named “Setup”. 

Navigate to “This PC -> Windows (C:) -> inetpub -> wwwroot -> osTicket -> include” and find the file named “ost-config.php” right click “ost-config.php” and select “properties” select “Security” select “Advanced” select “Everyone” select “Edit” and make sure that only the “Read” and “Read and execute” boxes are checked. Select OK, Select “Apply” Select OK.

Congratulations. 
  
You have successfully installed OsTicket. In the next tutorial we will go over how to configure OsTicket post-installation.
</p>

<br />
