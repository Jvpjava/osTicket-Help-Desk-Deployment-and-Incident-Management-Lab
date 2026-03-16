Below is the **clean GitHub Markdown version without horizontal lines**. GitHub automatically separates headings visually, so removing them makes the README look **cleaner and more professional**.

You can **paste this directly into your README.md**.

---

# osTicket Help Desk Deployment and Incident Management Lab

## Overview

This project demonstrates the deployment, configuration, and operational use of an **osTicket help desk system** hosted inside a **Microsoft Azure virtual machine environment**.

The lab simulates how enterprise IT departments manage support requests through a ticketing platform. The system was installed using **IIS, PHP, and MySQL**, configured for internal support operations, and tested by creating and resolving multiple support tickets.

The project covers three major phases:

1. Help desk system deployment
2. Post-installation system configuration
3. Real-world ticket lifecycle simulation

---

## Technologies Used

* Microsoft Azure
* Windows 10 Virtual Machine
* Internet Information Services (IIS)
* PHP 7.3
* MySQL 5.5
* HeidiSQL
* osTicket v1.15
* Remote Desktop Protocol (RDP)

---

## Environment Setup

The help desk system was hosted inside an **Azure Windows 10 virtual machine**.

### Infrastructure Components

* Azure Resource Group
* Windows 10 Virtual Machine (`osticket-vm`)
* IIS Web Server
* PHP runtime environment
* MySQL database server
* osTicket ticketing system

The VM was accessed remotely using **Remote Desktop Protocol (RDP)** to perform installation and configuration.

---

## Phase 1 — Help Desk System Deployment

### Creating the Virtual Machine

A Windows 10 virtual machine was deployed in **Microsoft Azure** to host the help desk system.

#### VM Configuration

```
VM Name: osticket-vm
Username: labuser
```

After deployment, the machine was accessed using **Remote Desktop** to begin installation.

---

### Installing the IIS Web Server

Internet Information Services (IIS) was enabled to host the osTicket web application.

#### Configuration Steps

1. Open **Windows Features**
2. Enable **Internet Information Services**
3. Enable **CGI under Application Development Features**

This allows IIS to execute **PHP applications required by osTicket**.

---

### Installing PHP and Required Dependencies

Several components were installed to support PHP applications.

#### Installed Components

* PHP Manager for IIS
* IIS URL Rewrite Module
* PHP 7.3 runtime
* Visual C++ Redistributable

A PHP runtime directory was created:

```
C:\PHP
```

The PHP runtime was registered inside IIS using **PHP Manager**.

---

### Installing MySQL Database

MySQL was installed to store help desk data including **users, tickets, and configuration settings**.

#### Database Configuration

```
Username: root
Password: root
```

A database management tool called **HeidiSQL** was installed to create and manage the osTicket database.

#### Database Created

```
osTicket
```

---

### Installing osTicket

The osTicket application files were installed inside the IIS web directory.

#### Installation Steps

1. Extract osTicket installation files
2. Copy the **upload** folder into:

```
C:\inetpub\wwwroot
```

3. Rename the folder:

```
upload → osTicket
```

4. Restart IIS

The osTicket installer was then accessed through the browser.

---

### Enabling Required PHP Extensions

Some PHP modules required by osTicket were initially disabled.

#### Enabled Extensions

```
php_imap.dll
php_intl.dll
php_opcache.dll
```

These modules allow **email integration, localization support, and improved performance**.

---

### Completing the Web Installer

The final installation was completed through the browser installer.

#### Database Configuration Used

```
Database Name: osTicket
Username: root
Password: root
```

#### Accessing the System

End User Portal

```
http://localhost/osTicket
```

Admin Portal

```
http://localhost/osTicket/scp/login.php
```

---

### Security Cleanup

After installation, setup files were removed to secure the system.

#### Removed Directory

```
C:\inetpub\wwwroot\osTicket\setup
```

#### Restricted Configuration File

```
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

Permissions were changed to **read-only**.

---

## Phase 2 — Help Desk System Configuration

After installing the platform, the help desk environment was configured to simulate a **real IT support organization**.

### Agent Panel vs Admin Panel

#### Agent Panel

Used by support technicians to:

* View assigned tickets
* Respond to users
* Troubleshoot issues
* Resolve incidents

#### Admin Panel

Used by administrators to configure:

* Agents and permissions
* Departments
* Teams
* SLA policies
* Help topics

---

### Configuring Roles

Roles define **permission levels for help desk agents**.

#### Navigation

```
Admin Panel → Agents → Roles
```

#### Role Created

```
Supreme Admin
```

This role provides **full administrative access**.

---

### Configuring Departments

Departments determine **which team handles a support request**.

#### Navigation

```
Admin Panel → Agents → Departments
```

#### Department Created

```
SysAdmins
```

Departments simulate real IT teams such as:

* System Administration
* Networking
* Help Desk Support

---

### Configuring Teams

Teams allow agents from multiple departments to collaborate on incidents.

#### Navigation

```
Admin Panel → Agents → Teams
```

#### Example Team

```
Online Banking
```

---

### Configuring Support Agents

Agents represent the technicians responsible for resolving tickets.

#### Navigation

```
Admin Panel → Agents → Add New
```

#### Agents Created

```
Jane (SysAdmins)
John (Support)
```

---

### Creating End Users

End users represent employees or customers requesting support.

#### Navigation

```
Agent Panel → Users → Add New
```

#### Users Created

```
Karen
Ken
```

---

### Configuring SLA Policies

Service Level Agreements define **response time requirements**.

#### Navigation

```
Admin Panel → Manage → SLA
```

#### Configured Policies

**Sev-A — Critical**

```
Response Time: 1 hour
Schedule: 24/7
```

**Sev-B — High Priority**

```
Response Time: 4 hours
Schedule: 24/7
```

**Sev-C — Standard**

```
Response Time: 8 hours
Schedule: Business Hours
```

---

### Configuring Help Topics

Help topics categorize incoming support tickets.

#### Navigation

```
Admin Panel → Manage → Help Topics
```

#### Topics Created

* Business Critical Outage
* Personal Computer Issues
* Equipment Request
* Password Reset
* Other

These categories help route tickets to the correct support teams.

---

## Phase 3 — Ticket Lifecycle Simulation

After deployment and configuration, the system was used to simulate **real help desk incidents**.

### Ticket Scenario 1 — Online Banking Outage

#### End User Ticket

```
Entire mobile/online banking system is down
```

Agent **John** reviewed the ticket and analyzed:

* Priority
* Department
* SLA
* Assigned technician

#### Ticket Classification

```
Priority: Sev-A
Response Time: 1 hour
Schedule: 24/7
```

The issue required escalation to **System Administration**, so the ticket was assigned to **Jane**.

Jane investigated the issue, resolved the outage, and closed the ticket.

---

### Ticket Scenario 2 — Accounting Software Issue

#### End User Request

```
Accounting department needs Adobe upgrade
```

#### Ticket Classification

```
Priority: Sev-B
Response Time: 4 hours
Department: Support
```

Agent **John** handled the issue and resolved the ticket.

---

### Ticket Scenario 3 — Executive Laptop Failure

#### End User Request

```
CFO’s laptop will no longer power on
```

#### Ticket Classification

```
Priority: Sev-B
Response Time: 4 hours
Department: Support
```

The issue was investigated and resolved by the help desk team.

---

### Observing Ticket Access Control

During testing, tickets assigned to the **SysAdmins department** became inaccessible to agents without proper permissions.

To resolve this:

1. Admin panel permissions were modified
2. John was granted **view access** to the SysAdmins department
3. Ticket visibility was restored

This demonstrates how **department permissions control access to sensitive incidents**.

---

## How Ticketing Systems Work in Real IT Environments

Most ticket systems integrate with **email notifications**.

When a ticket is updated:

* the user receives an email notification
* responses can be sent through email
* replies are automatically attached to the ticket

Tickets are typically created through:

* web portal
* email
* phone support
* chat systems
* walk-up requests

Even when issues are resolved immediately, support teams create tickets to **track work and maintain service metrics**.

---

## Skills Demonstrated

### Cloud Infrastructure

* Deploying Azure virtual machines
* Managing remote access using RDP

### Web Server Administration

* Installing and configuring IIS
* Hosting PHP applications

### Database Management

* Installing MySQL
* Managing databases using HeidiSQL

### Help Desk Administration

* Configuring support roles and permissions
* Managing departments and teams
* Implementing SLA policies

### Incident Management

* Ticket intake
* Ticket prioritization
* Incident escalation
* Troubleshooting and resolution

---

## Project Outcome

By completing this project, a **fully functional help desk system** was deployed and used to simulate real IT support operations.

This lab demonstrates the ability to:

* Deploy IT infrastructure
* Configure enterprise ticketing systems
* Manage support workflows
* Resolve and document technical incidents.
