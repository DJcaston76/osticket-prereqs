<img width="790" alt="Screenshot 2023-09-21 164350" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/0b1fa85e-edf1-4d3b-9fae-dd18a895b39c">
<h1>osTicket - Prerequisites and Installation</h1>
This is a guide of the installation and set up for the open-source ticketing software, osTicket. You can use this guide to follow along and even try it for yourself.<br />

<h2>Introduction to osTicket</h2>
<p>Using the osTicketing software, end users and IT Support agents can work together on support requests. In this guide, we’ll be installing osTicket, along with the necessary requirements for it to work properly for our use case.
</p>

<p>
In the upcoming guides, we’ll  be configuring the settings for the software and work through an example ticket.
</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Virtual Machine
- Microsoft Remote Desktop
- Internet Information Services (IIS)
- PHP 7.3.8 & MySQL

<h2>Operating Systems Used </h2>

- Windows 10, version 22H2

<h2>List of Prerequisites</h2>

- Microsoft Azure Virtual Machine
- osTicket Installation Files: [Installation Files](https://drive.google.com/drive/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)
- Heidi SQL

<br/>

<h2>Installation Steps</h2>

**Step 1: Create the VM within Microsoft Azure**
- Create a resource group called "RG-osTicket"
- Create a VM called "vm-osticket"
- Use Windows 10 Pro, version 22H2 and Standard_D4s_v3 - 2cpus, 16 GiB memory
- Make sure it auto populates to "RG-osTicket" for its resource group before the "Review and Create" step
- Note the username and password you're creating for your Windows 10 Virtual Machine

<br/>

<p>
<img width="812" alt="Screenshot 2023-09-21 115654" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/2ecbf674-28dc-47cc-b7c3-743f68fb97bb"></p>

**_These are recommended settings to use when creating your VM, depending on your location. Use a different location, if necessary._**

</p>

<p>
<img width="691" alt="Screenshot 2023-09-21 115326" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/330ab7f9-507e-4caa-9fbd-8793dcb77a3c"></p>

**_Make sure to checkmark the bottom part about licensing so you don't run into any issues._**

<br/>

**Step 2: Log into the VM via RDP**
- Copy the Public IP Address from the VM (Virutal Machines > "vm-osticket" > copy Public IP address)
- Log in, using your Windows 10 username and password

<br/>

<p>
<img width="835" alt="Screenshot 2023-09-21 120723" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/2dbc5354-9955-4815-b1c1-7530f19b78ed">
</p>

**_This what RDP looks like on a Windows. You'll use the username and password you created when you set up Windows in the VM, here._**

<br/>

**Step 3: Enable Internet Information Services (IIS)**
- Open IIS from the start menu (Right click start menu > Run > type in "control" > Programs > Programs and Features > Turn Windows Features on or off
- Under IIS > make sure Web Management Tools is enabled
- Under IIS > World Wide Web Services > Application Development Features, turn on CGI
- Under IIS > World Wide Web Services > Common HTTP Features, turn on all of the options here
- Click OK and allow it to install

<br/>

<p>
<img width="778" alt="Screenshot 2023-09-21 121239" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/a39b42e2-91a9-43f2-86b5-16925b75ec75">
</p>

**_Navigate to "Turn Windows Features on or off"._**

<p>
<img width="746" alt="Screenshot 2023-09-21 121653" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/e0aaebe8-aef0-43a8-a975-533d0816a30f">
</p>

**_Under Internet Information Services, make sure to turn on Web Management Tools if they're not checked._**

<br/>

**Step 4: Test IIS**
- Open a web broswer tab and type in "127.0.0.1"
- To ensure IIS enabled, you should see something similar to photo of the browser below
<br/>

<p>
<img width="797" alt="Screenshot 2023-09-21 122035" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/56b2020b-979f-44d2-b0cf-b80de338b4ce">
</p>

**_After installing IIS, it should look like the browser above._**

<br/>

**Step 5: Install the Requirements**
- Make sure to override any additional security prompts if you see them
- Download and install PHP Manager for IIS
- Download and install Rewrite Module
- Create C:\PHP directory by going to C: Drive > Right click > New > Folder > name it "PHP"
- Download PHP 7.3.8 files (be on the look for any extra prompts) > Right click > Extract All > Browse to the "PHP" folder > Extract
- Download and install VC Redistributable

<br/>

<p>
<img width="935" alt="Screenshot 2023-09-21 122649" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/73acfee5-ce2b-4b70-9f70-d56ed2b76b32">
</p>

**_When you're installing files, you'll need to accept their terms and make sure you download files onto your VM._**

<br/>

**Step 6: Install and Configure MySQL**
- Download and install MySQL 5.5.62
- Choose "Typical" installation
- Make sure to launch the Configuration Wizard
- Choose a "Standard Configuration"
- Use a simple password such as "Password1" _(Note: Always choose strong passwords in actual production.)_

<br/>

<p>
<img width="500" alt="Screenshot 2023-09-21 123716" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/90e1f489-5354-4fe8-bd09-5e292035bde4">

**_Make sure you launch the Configuration Wizard after installing MySQL._**
</p>

<br/>

**Step 7: Make Changes in the IIS Admin Panel**
- Search for IIS > Right click it to run it as admin
- At the "vm-osticket" level, open the PHP Manager > Select a principal > browse to and open the "php.cgi" file
- At the "vm-osticket" level, restart the server from the right sidebar menu

<br/>

<p>
<img width="1039" alt="Screenshot 2023-09-21 124242" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/355e1a40-e085-4ad2-809c-7558393c28f9">
</p>

**_Click "Register new PHP version"._**

<br/>

**Step 8: Install osTicket Files and Set Up Installer**
- Download osTicket files
- Open a 2nd file explorer window, navigate to C: > inetpub > wwwroot
- Drag the "Upload" folder from the osTicket files to "wwwroot" to copy files over
- Rename the file, from "Upload" to "osTicket"
- At rhe "vm-osticket" level in the admin for IIS, restart the server from the right sidebar menu again
- Navigate to Sites > Default > osTicket
- From the right sidebar, click "Browse *:80"

<br/>

<img width="1230" alt="Screenshot 2023-09-21 130439" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/2656485a-a037-4a49-9b84-1188527ff5d4">

**_Drag the "Upload" folder over to "wwwroot" and rename it to "osTicket"._**

<img width="1036" alt="Screenshot 2023-09-21 130832" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/f3a08ea9-6d98-4143-b6fc-dd13cf569233">

**_Click "Browse *:80" on the right sidebar so that it opens in the web browser._**

<br/>

**Step 9: Enabling PHP Extensions and Configuring File Permissions**
- Navigate back Sites > Default > osTicket in the admin IIS panel
- Open PHP Manager at this level and scroll down to click "Enable or disable an extension"
- Enable the following 3 extensions: php_imap.dll, php_intl.dll, and php.opcache.dll
- Refresh the osTicket Installer in your browser _(Note: you should see more checkmarks where it lists the extensions.)_
- Navigate to your C: Drive > inetpub > wwwroot > osTicket > Include > ost-sampleconfig.php
- Remove the "sample" part of the name, so that it reads "ost-config.php"
- Right click on the folder > Advanced > Disable Inheritance > Remove All
- Set New Permissions > Everyone (click "Check Names" to populate) > Check Full Control so that it applies all permissions

<br/>

<img width="601" alt="Screenshot 2023-09-21 154531" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/bdcdbb90-31e4-4631-a194-4b1554a1947e">

**_This is what it looks like before enabling the three PHP extensions._**

<img width="919" alt="Screenshot 2023-09-21 155149" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/23299144-3dd6-4cfb-8b41-4c0017f538a4">

**_Click "Full Control" for the "ost-config.php" file._**

<br/>

**Step 10: Continue Setting Up in the Browser**
- Click Continue
- Fill out each part of the form - choose a name, default email, and user information

<br/>

**Step 11: Install HeidiSQL**
- Download and open Heidi SQL
- Username will be "root", the password will be "Password1" _(Note: Choose strong passwords in actual production.)_
- Create a new session connection 
- Open a connection and right click to create a database called "osTicket"

<br/>

<img width="935" alt="Screenshot 2023-09-21 162242" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/11dad3ef-8615-4813-a1db-1f0f68b60a36">

**_Create a new database called "osTicket"._**

<br/>

**Step 12: Finish the Setup in the Broswer**
- Enter the following in the rest of the form
- MySQL DB: osTicket
- MySQL user/password: root/Password1
- Click Install Now

<br/>

<img width="606" alt="Screenshot 2023-09-21 162611" src="https://github.com/DJcaston76/osticket-prereqs/assets/145403292/a8833af1-880d-48d8-bc82-b06ba212dc3b">

**_Success! Make sure to copy these links for the next step._**

<h2>Next Steps</h2>

Now that the prerequisites are set up, continue to the second part for configuration.
[Post-install Configuration](https://github.com/DJcaston76/post-install-config)
