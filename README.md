# osTicket Help Desk System Deployment (Virtualbox + Windows IIS)

<p align="center">
  <img src="Lab 3 images/Part 1 images/Osticket Project Cover.png" width="700"/>
</p>

## Project Overview

Deployed a fully functional **osTicket help desk system** using a Windows server 2019 Virtual Machine.
Configured IIS, PHP, MySQL, and required dependencies to simulate a real-world IT support ticketing system.

This project demonstrates:

* System administration (Windows Server concepts on client OS)
* Web server configuration (IIS)
* Database setup (MySQL)
* Application deployment (osTicket)
* Troubleshooting and service validation

---

## Environment Setup

* **Platform:** VirtualBox
* **Virtual Machine:** Windows Server 2019
* **VM Name:** `DC-2019`
  
---

## Installation Steps

<p align="center">
  <img src="Lab 3 images/Part 1 images/Virtualbox banner.png" width="700"/>
</p>

### 1. Prepare the VM

* Go to Microsoft’s official **Windows Server 2019 Evaluation Center** page, sign in, register, and download the **ISO**. The evaluation version is listed as a **180-day trial** (Microsoft Evaluation Center: Windows Server 2019) ([Microsoft][1])

<p align="center">
  <img src="Lab 3 images/Part 1 images/Windows Evaluation Center ISO Download.png" width="700"/>
</p>

* Download and install **Oracle VirtualBox for Windows hosts** from the official VirtualBox downloads page (VirtualBox Downloads) ([VirtualBox][2])

  <p align="center">
    <img src="Lab 3 images/Part 1 images/Download Virtualbox.png" width="700"/>
  </p>

* Open VirtualBox and click **New**. Name the VM something like **Windows Server 2019**, set:
  <p align="center">
     <img src="Server2019Img/1. Create Server VM.png" width="700"/>
  </p>
   * **Type:** Microsoft Windows
   * **Version:** Windows 2019 (64-bit)
   <p align="center">
        <img src="Server2019Img/1. Server ISO Image and Name.png" width="700"/>
    </p>
* Give the VM hardware:

   * **RAM:** at least **4096 MB**
     <p align="center">
        <img src="Server2019Img/1. Server CPU & RAM.png" width="700"/>
     </p>
   * **CPU:** at least **2 cores**
     <p align="center">
        <img src="Server2019Img/1. Server CPU & RAM.png" width="700"/>
     </p>
   * Create a **virtual hard disk** with about **50–60 GB**
     <p align="center">
        <img src="Server2019Img/1. Server Storage.png" width="700"/>
     </p>

* Start the VM. The Windows installer will boot. Follow the setup steps:
  <p align="center">
    <img src="Server2019Img/1. Start your server.png" width="300"/>
  </p>

   * Pick language
  <p align="center">
    <img src="Server2019Img/2. Server Installation.png" width="700"/>
  </p>
   * Choose the edition you want
  <p align="center">
    <img src="Server2019Img/2. Server OS.png" width="700"/>
  </p>
   * Select **Custom Install** Install to the virtual disk
   <p align="center">
    <img src="Server2019Img/2. Server Drive.png" width="700"/>
  </p>

* After installation finishes, log in and install **VirtualBox Guest Additions** for better screen resizing, mouse support, and general VM use. VirtualBox provides Guest Additions through the VM menu and the included ISO (VirtualBox manual) ([VirtualBox][3])
  <p align="center">
    <img src="Server2019Img/2. Server installation Complete.png" width="700"/>
  </p>

  <p align="center">
    <img src="Server2019Img/2. Server Starting.png" width="700"/>
  </p>

  <p align="center">
    <img src="Server2019Img/3. Admin Password.png" width="700"/>
  </p>

  <p align="center">
    <img src="Server2019Img/3. Signin.png" width="700"/>
  </p>

  <p align="center">
    <img src="Server2019Img/4. Server Manager.png" width="700"/>
  </p>

  <p align="center">
    <img src="Server2019Img/2. Server installation Complete.png" width="700"/>
  </p>

  <p align="center">
    <img src="Server2019Img/4. Server Manager.png" width="700"/>
  </p>
Add Roles and Features
  <p align="center">
    <img src="Server2019Img/4. Add Roles and features.png" width="700"/>
  </p>
Click role based
  <p align="center">
    <img src="Server2019Img/4. Role based.png" width="700"/>
  </p>
For Roles use Active Directory Domain Services
  <p align="center">
    <img src="Server2019Img/4. Active Directory Domain Services.png" width="700"/>
  </p>
Add Features
  <p align="center">
    <img src="Server2019Img/5. Add Features.png" width="700"/>
  </p>
Install 
  <p align="center">
    <img src="Server2019Img/5. Install.png" width="700"/>
  </p>
Promote the server to a Domain Controller
 <p align="center">
    <img src="Server2019Img/5. Promote to DC.png" width="700"/>
  </p>
  Root Domain Name
   <p align="center">
    <img src="Server2019Img/6. Root domain name.png" width="700"/>
  </p>
  Domain Controller Password
   <p align="center">
    <img src="Server2019Img/6. DC Password.png" width="700"/>
  </p>
  Install Prerequesites
   <p align="center">
    <img src="Server2019Img/6. Install Prerequisites.png" width="700"/>
  </p>
  Server has to restart
   <p align="center">
    <img src="Server2019Img/6. AD Restart.png" width="700"/>
  </p>
  Sign into the domain controller
   <p align="center">
    <img src="Server2019Img/7. Signin to domain.png" width="700"/>
  </p>
  Go to server manager - Active directory users and computers
   <p align="center">
    <img src="Server2019Img/8. AD users and computers.png" width="700"/>
  </p>
  Verify Active directory users and computers is in domain GetHired
   <p align="center">
    <img src="Server2019Img/9. Domain GetHired Welcome.png" width="700"/>
  </p>

* Last step, set up networking in VirtualBox:
   * **Go to Devices and the network settings
 <p align="center">
    <img src="Server2019Img/9. Devices.png" width="700"/>
</p>
    * **host-only adapter** in network settings in virtualbox apply host-only adapter.
 <p align="center">
    <img src="Server2019Img/9. Network settings host adapter.png" width="700"/>
</p>

---

### 2. Enable IIS with CGI

* Open **Windows Server Roles Features**
* Enable:

  * Internet Information Services (IIS)
  * World Wide Web Services
<p align="center">
  <img src="Lab 3 images/Part 1 images/1. Enable Features with Server role IIS.jpg.png" width="700"/>
</p>

<p align="center">
  <img src="Lab 3 images/Part 1 images/1. Enable Features with Server role IIS.jpg.png" width="700"/>
</p>
  * Application Development Features
  * ✅ CGI

<p align="center">
  <img src="Lab 3 images/Part 1 images/2. Server Roles CGI.png" width="700"/>
</p>

---

### 3. Install Required Components

From installation folder:

* Install **PHP Manager for IIS**

<p align="center">
  <img src="Lab 3 images/Part 1 images/4. Install PHP Manager.png" width="700"/>
</p>

<p align="center">
  <img src="Lab 3 images/Part 1 images/4. Install PHP Manager Complete.png" width="700"/>
</p>
* Install **Rewrite Module**
<p align="center">
  <img src="Lab 3 images/Part 1 images/5. Install Rewrite Module.png" width="700"/>
</p>
<p align="center">
  <img src="Lab 3 images/Part 1 images/5. Install Rewrite Module 2.png" width="700"/>
</p>
* Install **VC++ Redistributable (x86)**
<p align="center">
  <img src="Lab 3 images/Part 1 images/8. Install VCRedist.png" width="700"/>
</p>
---

### 4. Configure PHP

* Create directory:

  ```
  C:\PHP
  ```

<p align="center">
  <img src="Lab 3 images/Part 1 images/6. Create a PHP Directory in C Drive.png" width="700"/>
</p>
  
* Extract:

  ```
  php-7.3.8-nts-Win32-VC15-x86.zip → C:\PHP
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/6. Extract PHP File in the PHP Folder.png" width="700"/>
</p>

<p align="center">
  <img src="Lab 3 images/Part 1 images/7. PHP Extract.jpg" width="700"/>
</p>
---

### 5. Install MySQL

* Install **MySQL 5.5.62**

<p align="center">
  <img src="Lab 3 images/Part 1 images/9. Install MySQL.png" width="700"/>
</p>

<p align="center">
  <img src="Lab 3 images/Part 1 images/9. MySQL Finish.png" width="700"/>
</p>
* Select:

  * Typical Setup
  * Launch Configuration Wizard

* Configuration:

  ```
  Username: root
  Password: root
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/9. MySQL Set up.png" width="700"/>
</p>
---

### 6. Configure IIS

* Open IIS as Administrator

<p align="center">
  <img src="Lab 3 images/Part 1 images/10. IIS.png" width="700"/>
</p>
<p align="center">
  <img src="Lab 3 images/Part 1 images/10. IIS Service.png" width="700"/>
</p>
* Go to **PHP Manager**

<p align="center">
  <img src="Lab 3 images/Part 1 images/11. PHP Manager in IIS.png" width="700"/>
</p>

* Register PHP:

  ```
  C:\PHP\php-cgi.exe
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/12. Register New PHP version.png" width="700"/>
</p>

<p align="center">
  <img src="Lab 3 images/Part 1 images/12. Register PHP Folder to the service.png" width="700"/>
</p>
* Restart IIS:

  * Stop → Start
 
<p align="center">
  <img src="Lab 3 images/Part 1 images/13. Reload IIS Service.png" width="700"/>
</p>

---

### 7. Install osTicket

* Extract:

  ```
  osTicket-v1.15.8.zip
  ```
* Copy **upload folder** to:

  ```
  C:\inetpub\wwwroot
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/osTicket zip to wwwroot.png" width="700"/>
</p>

* Restart IIS again

<p align="center">
  <img src="Lab 3 images/Part 1 images/Restart IIS.png" width="700"/>
</p>
---

### 8. Access Web Installer

Open in browser:

```
http://localhost/osTicket
```
<p align="center">
  <img src="Lab 3 images/Part 1 images/15. Browse http 80.png" width="700"/>
</p>

<p align="center">
  <img src="Lab 3 images/Part 1 images/16. Browser.png" width="700"/>
</p>
---

### 9. Enable Required PHP Extensions

In IIS:

* Go to:

  ```
  Sites → Default → osTicket → PHP Manager
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/17. Enable extensions in php manager.png" width="700"/>
</p>
Enable:

* php_imap.dll
* php_intl.dll
* php_opcache.dll

<p align="center">
  <img src="Lab 3 images/Part 1 images/17. PHP Extensions.png" width="700"/>
</p>

Refresh the browser and go to

* http://127.0.0.1/osTicket/setup/
<p align="center">
  <img src="Lab 3 images/Part 1 images/18. OsTicket website set up.png" width="700"/>
</p>


---

### 10. Configure osTicket Files

Rename config file:

```
C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
→ ost-config.php
```
<p align="center">
  <img src="Lab 3 images/Part 1 images/19. Change ost-config name.png" width="700"/>
</p>
Set permissions:

* Disable inheritance
* Remove all
<p align="center">
  <img src="Lab 3 images/Part 1 images/20. Assign permissions ost-config.png" width="700"/>
</p>
* Add:

  ```
  Everyone → Full Control
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/20. Everyone full control.jpg" width="700"/>
</p>
<p align="center">
  <img src="Lab 3 images/Part 1 images/20. Full control.png" width="700"/>
</p>
---

### 11. Database Setup (HeidiSQL)

* Install **HeidiSQL**

<p align="center">
  <img src="Lab 3 images/Part 1 images/22. Install heidiSQL.png" width="700"/>
</p>

* Create session:

  ```
  Username: root
  Password: root
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/24. New Session.png" width="700"/>
</p>
* Create database:

  ```
  osTicket
  ```
<p align="center">
  <img src="Lab 3 images/Part 1 images/25. Connect database.png" width="700"/>
</p>
<p align="center">
  <img src="Lab 3 images/Part 1 images/26. osTicket Database.png" width="700"/>
</p>
---

### 12. Complete Web Installation

In browser:

* Helpdesk Name: `Helpdesk`
* Default Email: (any valid email)

Database config:

```
Database: osTicket
Username: root
Password: root
```
<p align="center">
  <img src="Lab 3 images/Part 1 images/27. Connect heidi session with osTicket.png" width="700"/>
</p>
Click:

```
Install Now
```
<p align="center">
  <img src="Lab 3 images/Part 1 images/30. Congratulations osTicket has been configured.png" width="700"/>
</p>


* Refresh heidi: 
<p align="center">
  <img src="Lab 3 images/Part 1 images/29. osTicket refresh 2.png" width="700"/>
</p>
---

## ✅ Access URLs

* **Admin Panel:**

```
http://localhost/osTicket/scp/login.php
```
<p align="center">
  <img src="Lab 3 images/Part 1 images/32. Login to OSTICKET.png" width="700"/>
</p>
<p align="center">
  <img src="Lab 3 images/Part 1 images/33. osTicket web browser.png" width="700"/>
</p>

---

## 🧹 Post-Installation Cleanup

Delete setup folder:

```
C:\inetpub\wwwroot\osTicket\setup
```

Set config permissions to:

```
Read Only:
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```
