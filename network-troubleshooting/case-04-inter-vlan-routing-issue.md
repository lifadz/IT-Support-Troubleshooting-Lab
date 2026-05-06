# Case 04 - Unable to Reach Another Network Segment: Inter-VLAN Routing Issue

## Scenario

The finance department recently moved to a new floor. Their workstations were placed on VLAN 20 while the file server they need daily is on VLAN 10. After the move, finance users can browse the internet fine but cannot reach the file server at 192.168.10.50. Nothing was changed on the server side, only the user machines were relocated.

---

## Symptoms

- Finance users can ping devices within VLAN 20 without issues
- Finance users can reach the internet normally
- Finance users cannot ping 192.168.10.50 on VLAN 10
- tracert to 192.168.10.50 fails at the first hop or shows no path at all
- The issue started on the same day as the office move

---

## Troubleshooting Steps

**Step 1 - Check the user's current IP address and confirm which VLAN they are on**

```cmd
ipconfig /all
```

If the IP starts with 192.168.20.x, the machine is on VLAN 20. The file server is on 192.168.10.x which is a completely different subnet. Traffic between two different subnets requires routing and does not happen automatically.

> Screenshot suggestion: ipconfig showing 192.168.20.x address confirming VLAN 20

**Step 2 - Confirm internet access is working**

```cmd
ping 8.8.8.8
ping google.com
```

Both should succeed. If internet works, routing is partially functional. The problem is specifically cross-VLAN traffic, not a full connectivity failure.

**Step 3 - Try to ping the file server**

```cmd
ping 192.168.10.50
```

This is expected to fail. It confirms that cross-VLAN traffic is being dropped somewhere between the two VLANs.

**Step 4 - Run tracert to see where traffic stops**

```cmd
tracert 192.168.10.50
```

- One hop then timeouts means traffic is reaching the router or Layer 3 switch but being dropped there
- No hops at all means traffic is not even leaving the local network segment

> Screenshot suggestion: tracert output showing where the path breaks

**Step 5 - Check the router or Layer 3 switch configuration**

Log into the managed switch or router and check the following:

```
show ip route
show interfaces vlan 10
show interfaces vlan 20
show access-lists
```

Look for:
- Is there a route between VLAN 10 and VLAN 20?
- Is inter-VLAN routing enabled on the Layer 3 switch?
- Has the VLAN 20 interface been created and assigned an IP address?
- Are there any ACLs blocking traffic between these two VLANs?

**Step 6 - Verify the switch port VLAN assignment**

On the managed switch, check the port the finance PC is connected to:

```
show running-config interface gi0/5
```

It should show:
```
switchport mode access
switchport access vlan 20
```

If it shows a different VLAN, the traffic is being placed in the wrong segment.

**Step 7 - Verify the file server default gateway**

On the file server, confirm the default gateway is set to 192.168.10.1. Without a valid return path, ping replies from the server cannot get back to the finance client.

---

## Root Cause

When the finance team moved floors, the switch ports on the new floor were not pre-configured for VLAN 20. They were still set to VLAN 10 which was the default used for the server segment. On top of that, the Layer 3 switch had inter-VLAN routing configured for other VLANs but the VLAN 20 interface had never been created. There was no IP gateway for VLAN 20 traffic, so all cross-segment traffic was silently dropped.

---

## Solution

Created the VLAN 20 interface on the Layer 3 switch:

```
interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
```

Reassigned the finance floor switch ports to VLAN 20:

```
interface range gi0/1 - 24
 switchport mode access
 switchport access vlan 20
```

Updated the DHCP scope to issue 192.168.20.x addresses with gateway 192.168.20.1.

Reviewed the ACL and confirmed no rules were blocking VLAN 20 to VLAN 10 traffic.

Finance users ran the following to pick up new addresses:

```cmd
ipconfig /release
ipconfig /renew
```

File server access was restored immediately.

---

## Preventive Action

- Keep an updated network diagram with VLAN assignments per floor and per department
- Create a pre-move checklist that includes verifying switch port VLAN configurations before any relocation
- Test connectivity from a test device before the full office move happens
- Document all inter-VLAN routing rules and ACLs in a network runbook
- Always create and test the VLAN interface on the Layer 3 switch before moving users to a new VLAN

---

*[Back to README](../README.md)*
