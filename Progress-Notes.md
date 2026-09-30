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