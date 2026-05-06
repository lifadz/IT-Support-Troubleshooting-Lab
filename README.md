# IT Support Lab

A hands-on IT Support knowledge base and troubleshooting portfolio. This project documents real-world helpdesk scenarios, practical guides, and common fixes used in day-to-day IT Support work.

Everything here is written from a practical standpoint. The kind of stuff you actually deal with when supporting users, not just theory from a book.

---

## What's Inside

### Network Troubleshooting Cases

Step-by-step walkthroughs of real network issues, from no internet access to VLAN misconfigurations. Each case follows a structured format: symptoms, troubleshooting steps, root cause, fix, and prevention.

| # | Case | Category |
|---|---|---|
| 01 | [No Internet Access](./network-troubleshooting/case-01-no-internet-access.md) | Connectivity |
| 02 | [DHCP Failure - 169.254.x.x Address](./network-troubleshooting/case-02-dhcp-failure.md) | IP Addressing |
| 03 | [DNS Resolution Failure](./network-troubleshooting/case-03-dns-resolution-failure.md) | DNS |
| 04 | [Inter-VLAN Routing Issue](./network-troubleshooting/case-04-inter-vlan-routing-issue.md) | Routing |
| 05 | [Intermittent Network Drops](./network-troubleshooting/case-05-intermittent-network-drops.md) | Stability |

---

### IT Support Guides

Practical reference guides for common IT Support tasks.

| Guide | Description |
|---|---|
| [Network Setup](./guides/network-setup.md) | Setting up and verifying a basic network from scratch |
| [Software Installation](./guides/software-installation.md) | Installing common software and fixing installation errors |
| [Hardware Maintenance](./guides/hardware-maintenance.md) | Keeping hardware clean, healthy, and running well |
| [Security Best Practices](./guides/security-best-practices.md) | Basic security habits every IT Support engineer should follow |
| [How to Block Websites](./guides/how-to-block-websites.md) | Blocking unauthorized websites using the Windows hosts file |

---

### Common Troubleshooting

Quick reference for the most frequently reported issues in helpdesk environments.

| Issue | File |
|---|---|
| Computer won't start, slow performance, BSOD, printer issues | [common-troubleshooting.md](./common-troubleshooting.md) |

---

## Tools Used

| Tool | Purpose |
|---|---|
| `ipconfig` | Check IP address, subnet mask, gateway, and DNS |
| `ping` | Test connectivity to local and remote hosts |
| `tracert` | Trace the path packets take to a destination |
| `nslookup` | Test DNS name resolution |
| `arp -a` | Check ARP table and detect IP conflicts |
| `netsh` | View and configure network adapter settings |
| Windows Event Viewer | Review system and application error logs |
| Device Manager | Manage hardware drivers and device settings |
| CMD / PowerShell | Run diagnostic and configuration commands |

---

## Why This Project Exists

IT Support is a hands-on job. The best way to get better at it is to document your work, what the problem was, how you found it, and how you fixed it. This project is a record of that process.

It also serves as a portfolio to show that I can think through problems step by step, use the right tools, communicate clearly, and make sure issues do not keep coming back.

---

