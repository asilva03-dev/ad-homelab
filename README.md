# Active Directory Home Lab

This is a learning project to practice the day-to-day work of an IT help desk:
managing users, computers, permissions, and troubleshooting domain issues.
Using VirtualBox, I virtualized a Windows domain using Windows Server 2022 for
the domain controller and Windows 11 Enterprise for the client.

This lab simulates an IT environment for Random Play, a small fictional company.

## Environment Setup

- **Domain controller (DC01)**: 10.0.2.10 (static IP), Windows Server 2022
- **Domain-joined workstation (CLIENT01)**: DHCP, Windows 11 Enterprise
- **Hypervisor**: VirtualBox
- **Network**: NAT Network (10.0.2.0/24) so both virtual machines can speak to each other and the internet
- **Domain**: randomplay.local

## Progress

### Domain Controller

- Installed Windows Server 2022 and gave it a static IP of 10.0.2.10. The DC is
  also the DNS server, so its address can't change or clients would lose the
  ability to find the domain.
- Installed Active Directory Domain Services and promoted the server to the
  first domain controller of a new forest.
- DNS was installed during promotion and automatically created the SRV records
  clients use to locate the domain controller.

![DNS zone for randomplay.local](Screenshots/DNS.png)

### Client

- Installed Windows 11 Enterprise and pointed its DNS to the DC.
- Verified name resolution with nslookup before joining.
- Joined the randomplay.local domain and signed in with the domain Administrator account.

![CLIENT01 in Active Directory](Screenshots/ClientInAD.png)

## Bumps Along the Road

- Running nslookup returned "Server: UnKnown." The lookup still worked. The
  warning happens because there's no reverse lookup zone, so nslookup can't
  resolve the DNS server's IP back to a name.

## TODO

- OUs, users, and security groups for each department
- Help desk scenarios: password resets, lockouts, onboarding, offboarding
- Group Policy (password policy, mapped drives)
- Group-based shared folder permissions
- PowerShell script for bulk user creation