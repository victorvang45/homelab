# Active Directory
## Objective
The purpose of this lab is to practice Active Directory Basics

## Environment
- VirtualBox
- Windows Server 2022, Windows 11, Ubuntu Server 22.04

## Steps

### 1. Installed Active Directory Domain Services
- Opened Server Manager on Windows Server 2022
- Added the Active Directory Domain Services role
- Promoted server to Domain Controller
- Created domain: mydomain.com
- Restarted server to complete promotion

### 2. Configured DHCP Server
- Installed DHCP Server role through Server Manager
- Created a new DHCP scope
- Defined IP address range for client machines
- Authorized the DHCP server in Active Directory

### 3. Created Organizational Unit
- Opened Active Directory Users and Computers
- Created OU named Admins
- Used to organize and separate user accounts

![Organizational Unit admins created]
(assets/organizational-unit-create-admins.png)

### 4. Created Admin User
- Created dedicated admin account inside AD
- Assigned to Domain Admins group
- Used for day to day management instead of 
  default Administrator account

![Admin user accounts created]
(assets/create-admin-user.png)

### 5. Created Standard User Account
- Created a regular user account for testing
- Placed inside the OU named Users

![Standard user accounts created]
(assets/create-non-admin-user.png)

### 6. Verified Network Connectivity
- Logged into client Windows 11 VM with 
  standard user account
- Confirmed internet access working through 
  DHCP assigned IP address
- Verified domain join was successful

![Verify client1 is connected to domain on domain controller]
(assets/check-connection-on-dc.png)

![Verify client1 is connected to the internet via domain controller]
(assets/testing-connection-client1.png)

## Issues & Troubleshooting

**Potential issue to note:** Ensured client VM DNS 
was pointing to the Domain Controller IP address 
rather than router IP before joining the domain. 
This is a common misconfiguration that prevents 
domain joins from succeeding.

## What I Learned
- DHCP and Active Directory work together — the DC 
  hands out IP addresses to client machines while 
  simultaneously managing their user accounts and 
  permissions

- Organizational Units act like folders that let you 
  organize and manage users by department or role 
  rather than dumping everyone into one flat list

- Creating separate admin and standard user accounts 
  is best practice — you don't use the default 
  Administrator account for day to day tasks

- Joining a client machine to the domain and logging 
  in with a domain user account confirmed the whole 
  environment was communicating correctly
