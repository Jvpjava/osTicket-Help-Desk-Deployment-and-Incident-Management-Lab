# osTicket Help Desk System Deployment (Virtualbox + Windows IIS)

<p align="center">
  <img src="Lab 3 images/Part 1 images/Osticket Project Cover.webp" width="700" height="200"/>
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

* **Platform:** Microsoft Azure
* **Virtual Machine:** Windows Server 2019
* **VM Name:** `DC-2019`
* **Access Method:** Virtual Box

---

## Security Note

Passwords are shown for lab purposes only.
In real environments, always use a password manager such as:

* KeePass
* LastPass
* NordPass

---

## Installation Steps

### 1. Prepare the VM

* Go to Microsoft’s official **Windows Server 2019 Evaluation Center** page, sign in, register, and download the **ISO**. The evaluation version is listed as a **180-day trial** (Microsoft Evaluation Center: Windows Server 2019) ([Microsoft][1])

* Download and install **Oracle VirtualBox for Windows hosts** from the official VirtualBox downloads page (VirtualBox Downloads) ([VirtualBox][2])

* Open VirtualBox and click **New**. Name the VM something like **Windows Server 2019**, set:

   * **Type:** Microsoft Windows
   * **Version:** Windows 2019 (64-bit)

* Give the VM hardware:

   * **RAM:** at least **4096 MB**
   * **CPU:** at least **2 cores**
   * Create a **virtual hard disk** with about **50–60 GB**

* Go into the VM **Settings > Storage**, click the empty optical drive, and attach the **Windows Server 2019 ISO** you downloaded.

* Start the VM. The Windows installer will boot. Follow the setup steps:

   * Pick language
   * Click **Install now**
   * Choose the edition you want
   * Select **Custom Install**
   * Install to the virtual disk

* After installation finishes, log in and install **VirtualBox Guest Additions** for better screen resizing, mouse support, and general VM use. VirtualBox provides Guest Additions through the VM menu and the included ISO (VirtualBox manual) ([VirtualBox][3])

* Last step, set up networking in VirtualBox:

   * **NAT** if you just want internet inside the VM
   * **Bridged Adapter** if you want the VM to appear on your home network

---

### 2. Enable IIS with CGI

* Open **Windows Features**
* Enable:

  * Internet Information Services (IIS)
  * World Wide Web Services
  * Application Development Features
  * ✅ CGI

---

### 3. Install Required Components

From installation folder:

* Install **PHP Manager for IIS**
* Install **Rewrite Module**
* Install **VC++ Redistributable (x86)**

---

### 4. Configure PHP

* Create directory:

  ```
  C:\PHP
  ```
* Extract:

  ```
  php-7.3.8-nts-Win32-VC15-x86.zip → C:\PHP
  ```

---

### 5. Install MySQL

* Install **MySQL 5.5.62**

* Select:

  * Typical Setup
  * Launch Configuration Wizard

* Configuration:

  ```
  Username: root
  Password: root
  ```

---

### 6. Configure IIS

* Open IIS as Administrator

* Go to **PHP Manager**

* Register PHP:

  ```
  C:\PHP\php-cgi.exe
  ```

* Restart IIS:

  * Stop → Start

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

* Rename:

  ```
  upload → osTicket
  ```

* Restart IIS again

---

### 8. Access Web Installer

Open in browser:

```
http://localhost/osTicket
```

---

### 9. Enable Required PHP Extensions

In IIS:

* Go to:

  ```
  Sites → Default → osTicket → PHP Manager
  ```

Enable:

* php_imap.dll
* php_intl.dll
* php_opcache.dll

Refresh the browser

---

### 10. Configure osTicket Files

Rename config file:

```
C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
→ ost-config.php
```

Set permissions:

* Disable inheritance
* Remove all
* Add:

  ```
  Everyone → Full Control
  ```

---

### 11. Database Setup (HeidiSQL)

* Install **HeidiSQL**

* Create session:

  ```
  Username: root
  Password: root
  ```

* Create database:

  ```
  osTicket
  ```

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

Click:

```
Install Now
```

---

## ✅ Access URLs

* **Admin Panel:**

```
http://localhost/osTicket/scp/login.php
```

* **End User Portal:**

```
http://localhost/osTicket/
```

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

---

## 🔧 Troubleshooting (Real Issues Encountered)

**Issue: HTTP 404 when accessing osTicket**

* Cause: Incorrect folder structure or rename not done
* Fix: Ensure:

  ```
  upload → osTicket
  ```

  inside `wwwroot`

**Issue: PHP extensions not enabled**

* Cause: Missing required modules
* Fix: Enable in IIS PHP Manager

**Issue: MySQL not recognized**

* Cause: Service not running or PATH not set
* Fix:

  * Start MySQL service
  * Use full path to mysql.exe

---

## 💡 What This Project Shows

* Ability to deploy a full-stack web application
* Understanding of:

  * IIS (web server)
  * PHP (backend runtime)
  * MySQL (database)
* Real troubleshooting experience (404 errors, services, configs)
* Hands-on system administration in a cloud environment

---

## 📂 Suggested Repo Additions

To make this stand out more to recruiters:

* 📸 Screenshots:

  * IIS setup
  * osTicket UI
  * HeidiSQL database
* 📄 Diagram:

  * VM → IIS → PHP → MySQL → osTicket
* 🧠 Add a short reflection:

  * What broke
  * How you fixed it

---

If you want next step, I’ll:

* Turn this into a **killer GitHub README with badges + visuals**
* Help you write a **LinkedIn post that gets recruiter attention**
* Or review your screenshots and tell you exactly what to include
