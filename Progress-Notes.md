# Progress Log

## Session 1: DC01
- Installed VirtualBox 7.2 and downloaded eval ISOs from the Microsoft Evaluation Center
- Created LabNet (10.0.2.0/24) with VBoxManage because the GUI option wasn't showing
- Created DC01 (4GB, 2 CPU, 50GB) and switched the adapter from NAT to NAT Network
- Installed Server 2022 Desktop Experience, Guest Additions, renamed to DC01
- Static IP 10.0.2.10, gateway 10.0.2.1, DNS 127.0.0.1 (DC uses itself for DNS)
- Installed AD DS, promoted to DC for new forest randomplay.local

What I learned: why the DC needs a static IP, how DHCP assigns IPs, how the subnet mask decides
local vs gateway traffic, why clients must use the DC for DNS

## Session 2: CLIENT01 and domain join
- Created CLIENT01 (4GB, 2 CPU, 60GB, EFI on) with Windows 11 Enterprise
- Missed the boot prompt and landed in the EFI menu, fixed via Boot Manager
- Made a local account, set DNS to 10.0.2.10, left IP on DHCP
- nslookup randomplay.local returned 10.0.2.10
- Join failed: "specified username is invalid", fixed with RANDOMPLAY\Administrator
- Confirmed CLIENT01 in ADUC and its A record in DNS Manager

What I learned: what promotion and domain join actually do, local vs domain
accounts, cached credentials, why admins use separate accounts.

## Session 3: Building the company
- Wrote the first README and progress log and pushed them to GitHub
- Created the OU structure: RandomPlay > Users (IT, Sales, HR, Finance), Groups, Workstations
- Created 8 employee accounts, two per department, with temp passwords that must be changed at first logon
- Created asilva (standard) and adm-asilva (added to Domain Admins)
- Created IT-Staff, Sales-Staff, HR-Staff, and Finance-Staff groups and added users
- Logged into CLIENT01 as a standard user. Password change was rejected by the domain policy, fixed by using a password without the user's name
- Confirmed the standard user was denied access to Disk Management
- Moved CLIENT01 from the default Computers container into the Workstations OU
- Used Run as administrator as a standard user and approved the UAC prompt with adm-asilva

What I learned: the difference between the network and the domain, how
DHCP and the subnet relate, OUs vs groups, built-in groups like Domain Users
and Domain Admins, what happened to the local Administrator during promotion,
the default password policy, and how admin rights on a workstation come from
Domain Admins being nested in its local Administrators group