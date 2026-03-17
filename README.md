# osTicket Help Desk Deployment — Part 1 (System Installation)

## Overview

This phase of the project focuses on deploying the **osTicket help desk system** inside a **Windows 10 Azure Virtual Machine**.

The objective was to build the full backend environment required to run a production-style ticketing system, including:

* Web server configuration (IIS)
* PHP runtime setup
* MySQL database installation
* osTicket application deployment

This simulates how IT teams deploy internal support systems in real environments.

This implementation followed a structured lab process. 

---

# Environment Setup

## Azure Virtual Machine Configuration

A Windows 10 virtual machine was created in Microsoft Azure.

```bash
VM Name: osticket-vm
Username: labuser
```

The system was accessed using **Remote Desktop Protocol (RDP)** to perform all configurations.

---

# Web Server Configuration (IIS)

Internet Information Services (IIS) was installed to host the osTicket web application.

### Features Enabled

* Web Server (IIS)
* Application Development Features
* CGI (Required for PHP execution)

This allows IIS to process dynamic PHP content required by osTicket.

---

# PHP Installation and Configuration

To support osTicket, PHP and required modules were installed.

### Components Installed

* PHP Manager for IIS
* URL Rewrite Module
* PHP 7.3 Runtime
* Microsoft Visual C++ Redistributable

### Directory Setup

```bash
C:\PHP
```

PHP was registered in IIS using:

```bash
php-cgi.exe
```

IIS was restarted to apply changes.

---

# Database Installation (MySQL)

MySQL was installed to handle ticket data, user records, and system configuration.

### Configuration

```bash
Username: root
Password: root
```

---

## Issue Encountered — MySQL Access Denied

### Problem

During setup, MySQL failed with:

```bash
Error 1045: Access denied for user 'root'@'localhost'
```

### Cause

* Previous MySQL installation data remained on the system
* Old configuration conflicted with new credentials

### Fix

* Fully uninstalled MySQL
* Deleted leftover directories:

```bash
C:\ProgramData\MySQL
```

* Reinstalled MySQL using standard configuration
* Verified login via command line

This reflects real-world troubleshooting of **service configuration conflicts**.

---

# osTicket Application Installation

The osTicket application was deployed into the IIS web directory.

### Directory Path

```bash
C:\inetpub\wwwroot\osTicket
```

The application files were extracted and placed correctly inside this directory.

IIS was restarted after deployment.

---

## PHP Extensions Enabled

The following extensions were required for osTicket functionality:

```bash
php_imap.dll
php_intl.dll
php_opcache.dll
```

These support:

* Email handling
* Internationalization
* Performance optimization

---

# Configuration File Setup

The default configuration file was renamed:

```bash
ost-sampleconfig.php → ost-config.php
```

### Permissions Applied

* Disabled inheritance
* Assigned full control (temporary for setup)

This allows the web installer to write configuration settings.

---

# Database Connection Setup

Using **HeidiSQL**, a database was created:

```bash
Database Name: osTicket
```

This database was linked during the web-based installation.

---

# Accessing osTicket

### Admin Portal

```bash
http://localhost/osTicket/scp/login.php
```

### End User Portal

```bash
http://localhost/osTicket/
```

---

# Issue Encountered — HTTP 404 Error

### Problem

Accessing the admin login page returned:

```bash
HTTP 404 – Not Found
```

### Cause

* Incorrect folder structure
* osTicket files were nested inside an extra `upload` directory
* IIS could not locate required files like:

```bash
scp/login.php
```

### Fix

* Moved all contents from the `upload` folder directly into:

```bash
C:\inetpub\wwwroot\osTicket
```

* Ensured directories like `scp`, `include`, and `api` were at the root level

After correcting the structure, the site loaded successfully.

---

# Post-Installation Security

After successful installation, cleanup and security hardening steps were performed.

### Removed Setup Directory

```bash
C:\inetpub\wwwroot\osTicket\setup
```

### Secured Configuration File

```bash
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

Permissions set to:

* Read-only

This prevents unauthorized modifications.

---

# Skills Demonstrated

### System Administration

* Windows Server configuration
* IIS setup and management

### Web Hosting

* Hosting PHP applications on IIS
* Configuring application dependencies

### Database Management

* MySQL installation and troubleshooting
* Database creation and integration

### Troubleshooting

* Resolving service authentication errors
* Fixing web server directory structure issues

### Security Practices

* Removing installation artifacts
* Securing configuration files

---

# Outcome

This phase demonstrates the ability to deploy a fully functional help desk system from scratch, including all required backend services.

The system is now ready for:

* Help desk configuration
* User and role setup
* Ticket lifecycle management

---

If you want next level improvement, I can combine this with Part 2 and 3 later into a **single polished portfolio project** that looks like real enterprise documentation instead of separate labs.
