# Case 01 - No Internet Access: User Cannot Browse

## Scenario

A user submits a helpdesk ticket on a Monday morning saying they cannot access any websites. Their computer is connected to the office network via Ethernet and the network icon in the taskbar shows no warning. Other users in the same area are online without any issues.

---

## Symptoms

- Browser shows "This site can't be reached" or "No internet connection"
- All websites are unreachable, not just one
- Network icon shows connected with no red X or exclamation mark
- Other computers in the same area are working fine
- User says it was working fine the day before

---

## Troubleshooting Steps

**Step 1 - Confirm the issue is isolated to this machine**

Ask the user: "Is anyone else in your area having the same problem?" If the answer is no, this is likely a device-specific issue and not a network-wide outage.

**Step 2 - Check the physical connection**

- Is the Ethernet cable plugged in securely at both ends?
- Is the link light on the NIC and the switch port blinking green?
- Try reseating the cable or swapping it with a known-good one

**Step 3 - Run ipconfig /all to check the IP configuration**

```cmd
ipconfig /all
```

Look for:
- A valid IP address (e.g., 192.168.1.x)
- Correct subnet mask (e.g., 255.255.255.0)
- A default gateway (e.g., 192.168.1.1)
- DNS server entries

> Screenshot suggestion: Capture the full ipconfig /all output here

**Step 4 - Ping the default gateway**

```cmd
ping 192.168.1.1
```

If this fails, the device cannot reach the local network. The problem is between the device and the router or switch.

If this succeeds, move to Step 5.

**Step 5 - Ping a public IP address**

```cmd
ping 8.8.8.8
```

This test bypasses DNS completely. If 8.8.8.8 responds but websites still won't load, the issue is DNS-related. If 8.8.8.8 also fails, the problem is with internet routing or the ISP.

> Screenshot suggestion: Show ping results to the gateway and to 8.8.8.8

**Step 6 - Run tracert to see where packets stop**

```cmd
tracert 8.8.8.8
```

Look at which hop fails. If packets stop at the first hop, the router is the issue.

**Step 7 - Flush DNS and release/renew the IP**

```cmd
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

**Step 8 - Restart the network adapter**

Go to Network Adapter Settings, disable the adapter, then enable it again. This clears any stuck state on the NIC.

**Step 9 - Restart the machine**

If none of the above steps fix it, restart the computer. The Windows networking stack can sometimes get into a bad state.

---

## Root Cause

The DNS server entries were blank. They were accidentally cleared when a colleague manually changed network settings on the machine. The IP address and gateway were valid, which is why the network icon showed no warning. Without DNS, no hostnames could resolve and no websites could load.

---

## Solution

Added the correct DNS server addresses manually:
- Primary DNS: 8.8.8.8 (Google) or the internal company DNS server
- Secondary DNS: 8.8.4.4

Steps taken:
1. Go to Network Adapter, Properties, IPv4
2. Select "Use the following DNS server addresses"
3. Enter the DNS values above
4. Run `ipconfig /flushdns`
5. Tested with `ping google.com` and confirmed it resolved successfully

Browsing was restored immediately.

---

## Preventive Action

- Push DNS settings via DHCP so they are assigned automatically and cannot be accidentally overwritten
- Lock down manual network configuration on user machines via Group Policy
- Document the correct DNS server addresses in the network runbook

---

*[Back to README](../README.md)*
