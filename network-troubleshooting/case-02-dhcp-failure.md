# Case 02 - DHCP Failure: Device Gets APIPA Address (169.254.x.x)

## Scenario

A new laptop was just added to the office network. The user plugs it in and immediately calls saying they cannot access anything, not even the internal file server. You check and find the machine has an IP address starting with 169.254.x.x.

---

## Symptoms

- IP address shows as 169.254.x.x (APIPA range)
- Cannot reach any internal resources or the internet
- No default gateway shown in ipconfig
- Ethernet cable is physically connected
- Other machines on the same switch are working fine

---

## Troubleshooting Steps

**Step 1 - Run ipconfig /all and confirm the APIPA address**

```cmd
ipconfig /all
```

A 169.254.x.x address means Windows could not reach a DHCP server and assigned itself a random IP. This is the first clue.

> Screenshot suggestion: Show ipconfig output with the 169.254.x.x address

**Step 2 - Check the physical layer first**

- Is the Ethernet cable plugged in at both ends?
- Is the NIC showing a link light on the port?
- Try a different cable and a different switch port

**Step 3 - Try to manually renew the DHCP lease**

```cmd
ipconfig /release
ipconfig /renew
```

Watch the output carefully:
- "Media disconnected" means the NIC is not seeing the network, which is a physical issue
- Request times out means the DHCP server is not responding

**Step 4 - Test with another device on the same switch port**

Plug in a laptop you know works. Does it get a valid IP?
- Yes means the DHCP server is fine and the issue is with this specific device
- No means the DHCP server or switch port VLAN configuration is the problem

**Step 5 - Check the DHCP server or router**

Log into the router or DHCP server and check:
- Is the DHCP service running?
- Is the lease pool full with no free addresses left?
- Are there stale leases from old or decommissioned devices taking up slots?

**Step 6 - Assign a static IP temporarily to confirm the network itself works**

- IP: 192.168.1.200 (an unused address in range)
- Subnet: 255.255.255.0
- Gateway: 192.168.1.1
- DNS: 8.8.8.8

If connectivity is restored with a static IP, DHCP is confirmed as the issue and not the machine or cable.

---

## Root Cause

The DHCP lease pool on the router was exhausted. The office recently added several IoT devices including printers and smart TVs in meeting rooms. The default pool of 50 addresses was completely used up. Stale leases from decommissioned devices were still occupying slots, leaving no free addresses for the new laptop.

---

## Solution

1. Logged into the router admin panel
2. Identified stale leases from old printers and a replaced PC
3. Cleared the stale leases to free up addresses
4. Expanded the DHCP pool range to accommodate future growth
5. Ran the following on the user's laptop:

```cmd
ipconfig /release
ipconfig /renew
```

The laptop received a valid IP immediately. Connectivity restored.

---

## Preventive Action

- Regularly audit the DHCP lease table and remove stale or inactive entries
- Set appropriate lease durations, shorter for guest networks and longer for fixed workstations
- Monitor DHCP pool utilization and set an alert when it hits 80% capacity
- Use DHCP reservations for servers and printers so they do not consume dynamic pool addresses

---

*[Back to README](../README.md)*
