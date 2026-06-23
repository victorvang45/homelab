# Active Directory
## Objective
The purpose of this lab is to practice Active Directory Basics.

## Environment
- VirtualBox
- TryHackMe VMs
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

![Organizational Unit admins created](assets/organizational-unit-create-admins.png)

*Organizational Unit admins created*

### 4. Created Admin User
- Created dedicated admin account inside AD
- Assigned to Domain Admins group
- Used for day to day management instead of 
  default Administrator account

![Admin user accounts created](assets/create-admin-user.png)

*Admin user accounts created*

### 5. Created Standard User Account
- Created a regular user account for testing
- Placed inside the OU named Users
  
![Standard user accounts created](assets/create-non-admin-user.png)

*Standard user accounts created*

### 6. Verified Network Connectivity
- Logged into client Windows 11 VM with 
  standard user account
- Confirmed internet access working through 
  DHCP assigned IP address
- Verified domain join was successful

![Verify client1 is connected to domain on domain controller](assets/check-connection-on-dc.png)

*Verify client1 is connected to domain on domain controller*

![Verify client1 is connected to the internet via domain controller](assets/testing-connection-client1.png)

*Verify client1 is connected to the domain controller and internet*

### 7. Delegated Password Reset Permissions
- Selected a standard user to act as helpdesk staff
- Delegated permission to reset passwords and 
  force password change at next login
- Verified delegated user could reset passwords 
  without full admin access

![Delegation of Control wizard](assets/delegation-control.png)

*Giving Philip persmission to reset passwords and force password reset next login*

### 8. Configured OU Deletion Protection
- Enabled accidental deletion protection on OUs
  during creation
- Practiced disabling protection in order to 
  delete an OU
- Noted this is a best practice to prevent 
  accidental removal of critical directory objects

![OU protection settings](assets/ou-deletion-protection.png)

*Showing that IT is protected from deletion. To delete, we would have to uncheck that box*

## Issues & Troubleshooting

**No critical issues encountered during initial setup.**

However the following are common issues to be aware 
of in this environment:

- **OU deletion fails** — caused by accidental 
  deletion protection being enabled. Fix: go to 
  View → Advanced Features in AD Users and 
  Computers, then uncheck the protection box in 
  the OU properties

- **Delegation not applying correctly** — verify 
  the correct OU was selected during the Delegation 
  of Control wizard and that the user account is 
  in the right group

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

- OUs have an accidental deletion protection setting 
  that must be manually disabled before the OU can 
  be removed — an important safeguard in real 
  environments where mistakes are costly

- Delegation of Control allows specific users to 
  perform limited admin tasks like password resets 
  without being granted full Domain Admin privileges 

- Disabling a user account rather than deleting it 
  is best practice when an employee leaves — the 
  account and its history are preserved in case 
  they're needed later
