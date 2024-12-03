<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10 Pro </b> (22H2), at least 2vCPUs, 8GB RAM

<h2>List of Prerequisites</h2>

- <b>PHP manager for IIS</b> - ensures PHP is correctly configured to run IIS
- <b>Rewrite module </b> - facilitates URL rewriting and redirect users to URLs
- <b>VC_redist.x86</b> (redistributable) - osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly
- <b>MySQL</b> - for storing data into databases
- <b>HeidiSQL</b> - interface for accessing MySQL 


<h2>Installation Steps</h2>
<p>
Once your Windows 10 virtual machine is running in Azure, log in using your credentials.  (Remember to keep a record of all usernames and passwords used during this lab, as you'll need them later.)  Open the Edge browser within the VM and download the osTicket installation files from this link. After the download is complete, extract the contents of the zip file. You should see the following files
</p>
<br />

<p>
<img src="https://i.imgur.com/29gqX2m.png" height="80%" width="80%" alt="extracted osticket zip file"/>
</p>


<p>
Enable Internet Information Services (IIS) by going to Control Panel > Uninstall a program > Turn Windows features on or off.  Make sure to also enable CGI under World Wide Web Services > Application Development Features.
</p>
<br />

<p>
<img src="https://i.imgur.com/CdojXsp.png" height="80%" width="80%" alt="enable IIS and CGI"/>
</p>
<br/>
<p>
Install the PHP Manager for IIS by running the downloaded installer and accepting the default options. Similarly, install the rewrite modules by running the rewrite_amd64 installer with default settings.


</p>
<img src="https://i.imgur.com/Uh4Zwlj.png" height="80%" width="80%" alt="install php manager and rewrite"/>

<br />

<p>
Create a new folder named "PHP" in the C:\ drive (C:\PHP). You can access the drive through File Explorer. This folder will store the extracted PHP files, which are essential for osTicket to function correctly.
</p>
<p>
  <img src="https://i.imgur.com/BCMLUId.png" height="80%" width="80%" alt="extract php to c php"/>
</p>
<br/>

<p>
Install the  Redistributable package with default settings. Then install MySQL using the "Standard Configuration" option. For simplicity, set the username and password to "root" during the MySQL installation (in a real-world scenario, use a stronger password).
</p>
<p>
  <img src="https://i.imgur.com/dbDt0um.png" height="50%" width="50%" alt="install redistr and mysql"/>
</p>
<br/>

<p>
Open Internet Information Services (IIS) as administrator (search for "IIS" and select "Run as administrator").  In IIS Manager, click on "PHP Manager" and then "Register new PHP version." Select the  C:\PHP\php-cgi.exe file.
  
</p>
<p>
  <img src="https://i.imgur.com/3twI19f.png" height="80%" width="80%" alt="configure PHP new version in PHP manager"/>
</p>
<br/>

<p>
To apply the PHP configuration changes, you need to restart IIS. In the Actions pane on the right-hand side of the IIS Manager window, click "Stop" to stop the IIS service. Then, click "Start" to restart it. This will load the new PHP version you just registered.
</p>
<p>
  <img src="https://i.imgur.com/iO7K6aO.png" height="30%" width="30%" alt="reload IIS"/>
</p>
<br/>

<p>
Extract the contents of the osTicket zip file. Move the upload folder from the extracted files to C:\inetpub\wwwroot and rename it to osTicket (it must  be exact).
  
</p>
<p>
  <img src="https://i.imgur.com/xJw174Y.png" height="80%" width="80%" alt="extract osticket zipped folder and move to wwwroot"/>
</p>
<br/>

<p>
Reload IIS again. On the left side pane, go to Sites, click the down arrow until you reach osTicket and then click on Browse in the right side pane, then you should get this.
</p>
<p>
  <img src="https://i.imgur.com/4ahLEvm.png" height="80%" width="80%" alt="osticket landing page"/>
</p>
<br/>
<p>
Now we'll need to enable some extensions. Go back to the osTicket folder on the left side pane and then click on PHP manager in the middle pane. Click on Enable or disable an extension and you'll need to enable php_imap.dll, php_intl.dll and php_opcache.dll. Refresh the osTicket webpage and it should be updated.
</p>
<p>
  <img src="https://i.imgur.com/87i9Gxs.png" height="80%" width="80%" alt="updated osticket landing page"/>
</p>
<br/>
<p>
Now we have to rename C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php to C:\inetpub\wwwroot\osTicket\include\ost-config.php. Then we'll need to change permissions for this file. Right click on this and then Properties -> Security tab -> Advanced -> Disable inheritance (remove option) -> Add -> Select a principal -> Type everyone in the box -> Check names -> OK. Make sure you click on Full control as well.
</p>
<p>
  <img src="https://i.imgur.com/wABTm3C.png" height="80%" width="80%" alt="ost config permissions"/>
</p>
<br/>
<p>
In the osTicket setup page, click "Continue" and fill in the desired login details for the helpdesk.  Ensure the MySQL database name is "osTicket" and the username/password are "root"/"root". Before proceeding, install HeidiSQL from the extracted osTicket files, accepting all defaults. Create a new session in HeidiSQL, connect to the database with "root"/"root", and create a new database named "osTicket".
</p>
<p>
  <img src="https://i.imgur.com/Lfw0PXJ.png" height="80%" width="80%" alt="heidisql"/>
  <img src="https://i.imgur.com/pWKEjjz.png" height="80%" width="80%" alt="create new database in heidisql"/>
</p>
On the osTicket setup page, click "Install Now" to complete the installation. You'll be presented with a confirmation page containing links to access osTicket as a user (
http://localhost/osTicket) or as staff (http://localhost/osTicket/scp).
<br/>
<p>
   <img src="https://i.imgur.com/CBKO7Qs.png" height="80%" width="80%" alt="osticket installed"/>
</p>
