# HomeLab

Personal cybersecurity and IT infrastructure lab for hands-on practice with Active Directory administration,
Windows Server, networking, virtualization, firewalls, Group Policy, file services and security monitoring.
Built to support continuous learning and practical enterprise IT experience.

> 🚧 **Work in progress.** Write-ups, screenshots and configs are being added section by section.
> See the [checklist](#-documentation-checklist) below.

## Lab topology

Source diagram: [`diagrams/network-topology.drawio`](diagrams/network-topology.drawio) (open with [diagrams.net](https://app.diagrams.net)).

| Host | Role | OS / platform | IP |
|---|---|---|---|
| OPNsense | Firewall / gateway | OPNsense | 10.10.10.1/24 |
| DC01 | Domain controller (AD, DNS, DHCP) | Windows Server | 10.10.10.10 |
| DC02 | Domain controller (AD, DNS, DHCP failover) | Windows Server | 10.10.10.11 |
| WINClient-01 | Domain-joined workstation | Windows 10 | 10.10.10.153 |
| UBU_DC02 | Linux server | Ubuntu Server | 10.10.10.125 |
| Kali-01 | Attack / assessment box | Kali Linux | 10.10.10.105 |

Lab network: `10.10.10.0/24` (private, isolated lab addressing).

## Services
- Active Directory Domain Services (two domain controllers)
- DNS (AD-integrated, replicated between DCs)
- DHCP with failover
- Group Policy
- SMB file services (departmental shares)

## Completed so far
From the [lab overview](docs/lab-overview.md):
- Built redundant domain controllers
- Configured DNS replication
- Implemented DHCP failover
- Deployed OPNsense firewall
- Created departmental shares
- Configured drive mapping via GPO

## Roadmap
- [ ] Deploy Wazuh SIEM
- [ ] Install Sysmon
- [ ] Add Kali Linux
- [ ] Perform vulnerability assessments

## Repository structure
```text
.
├── README.md
├── diagrams/
│   └── network-topology.drawio   # editable lab diagram
└── docs/
    └── lab-overview.md           # environment, services, achievements, roadmap
```

## 📋 Documentation checklist
Things to add (screenshots and configs only I have). **Remove anything sensitive first:** passwords,
public IPs, MAC addresses, license keys, real usernames or domain names I don't want public.

**Diagram**
- [ ] Export `diagrams/network-topology.drawio` to PNG/SVG (`diagrams/network-topology.png`) and embed it at the top of this README

**Hyper-V / virtualization** (`docs/hyper-v.md`)
- [ ] Host specs and virtual switch layout (internal/external/private)
- [ ] Screenshot of the VM list in Hyper-V Manager

**Windows Server & Active Directory** (`docs/active-directory.md`)
- [ ] Domain name/functional level (or a placeholder), OU structure, users/groups created
- [ ] Screenshots: AD Users and Computers OU tree, DC replication healthy (`repadmin /replsummary`)
- [ ] Any PowerShell used to create OUs/users/groups (`scripts/`)

**DNS & DHCP failover** (`docs/dns-dhcp.md`)
- [ ] DHCP scope settings and failover mode (load balance / hot standby)
- [ ] Screenshots: DNS zones, DHCP failover relationship status
- [ ] How failover was tested (e.g., stopping DHCP on DC01) and what happened

**Group Policy** (`docs/group-policy.md`)
- [ ] GPOs created (drive mapping, security settings) and where they're linked
- [ ] Screenshot of GPMC + `gpresult /r` on WINClient-01
- [ ] Optional: exported GPO reports (HTML) with sensitive values removed

**File services** (`docs/file-services.md`)
- [ ] Departmental share layout and NTFS/share permission model
- [ ] Screenshot of mapped drives on the client

**OPNsense** (`docs/opnsense.md`)
- [ ] Interfaces, firewall rule summary, NAT/DNS settings
- [ ] Screenshots of the dashboard and rules (redact WAN/public IP)
- [ ] Optional: sanitized config export (remove password hashes and keys)

**Security monitoring (roadmap)** (`docs/wazuh.md`, `docs/sysmon.md`)
- [ ] Wazuh manager/agent deployment steps and dashboard screenshots
- [ ] Sysmon config used
- [ ] Test detections (what was done → what alert fired)

**Lessons learned** (`docs/lessons-learned.md`)
- [ ] Problems hit and how they were fixed (great interview material)
