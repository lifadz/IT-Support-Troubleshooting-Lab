# Case 05 - Intermittent Network Drops: User Keeps Losing Connection

## Scenario

A user reports their connection keeps dropping every 20 to 30 minutes throughout the day. Each time it drops, they lose access to the shared drive, VoIP calls get cut off, and they have to wait about a minute or two before the connection comes back on its own. This has been happening for three days and no other users nearby are affected.

---

## Symptoms

- Connection drops periodically, not constant but consistent every 20 to 30 minutes
- All network activity stops during the drop including shared drives, internet, and VoIP
- Connection comes back on its own after 1 to 2 minutes without any action
- No error messages appear, the network icon briefly shows disconnected
- Problem is specific to this one machine
- Issue has been ongoing for three days

---

## Troubleshooting Steps

**Step 1 - Rule out a network-wide issue**

Check if anyone else has reported drops. Look at monitoring tools or open helpdesk tickets. If this is isolated to one user, focus on their machine and physical connection, not the switch or router.

**Step 2 - Run a continuous ping to capture the drops in real time**

While the user continues working normally, run a long-running ping to the gateway:

```cmd
ping 192.168.1.1 -t
```

The -t flag keeps it running until you stop it. When the drop happens, you will see a burst of "Request timed out" responses. This captures exactly when the drop occurs and how long it lasts.

**Step 3 - Inspect the physical cable and switch port**

- Look at the Ethernet cable for any kinks, sharp bends, or visible damage
- Replace it with a brand new cable
- Move the connection to a different switch port
- On a managed switch, check the port statistics:

```
show interface gi0/5
```

High CRC error counts or input errors on the port suggest a bad cable or a failing NIC.

**Step 4 - Check NIC power management settings**

This is one of the most commonly missed causes of intermittent drops on Windows machines.

1. Open Device Manager
2. Expand Network Adapters
3. Right-click the NIC and select Properties
4. Go to the Power Management tab
5. Uncheck "Allow the computer to turn off this device to save power"
6. Click OK

> Screenshot suggestion: NIC Power Management tab with the checkbox highlighted

Windows can aggressively power down the NIC during low traffic periods. The wake-up delay causes the 1 to 2 minute reconnection window that users experience.

**Step 5 - Check Windows Event Viewer for NIC errors**

Open Event Viewer, go to Windows Logs, then System. Filter by your NIC driver name such as e1iexpress or Intel Ethernet. Look for warning or error events that match the times the user reported drops.

**Step 6 - Update the NIC driver**

1. Open Device Manager, right-click the NIC, select Properties
2. Go to the Driver tab and note the current driver version and date
3. Visit the manufacturer website (Intel, Realtek, Broadcom) and check for a newer version
4. Install the update and restart

Outdated NIC drivers are a known cause of intermittent disconnections, especially after Windows updates.

**Step 7 - Test with a USB network adapter**

Temporarily replace the built-in NIC with a USB-to-Ethernet adapter. If the drops stop immediately, the onboard NIC is the hardware fault.

**Step 8 - Check for IP address conflicts**

```cmd
arp -a
```

Compare the MAC address tied to your IP with the actual NIC MAC shown in ipconfig /all. A mismatch means another device on the network has the same IP, which causes periodic connection interruptions.

---

## Root Cause

The NIC power management setting was configured to allow Windows to turn it off during low traffic periods. The machine's power saving profile was shutting down the NIC after a period of inactivity. When new network traffic arrived, the NIC needed 60 to 90 seconds to fully wake back up, which caused the periodic reconnection window the user kept experiencing.

---

## Solution

1. Opened Device Manager, went to Network Adapters, opened NIC Properties
2. Under the Power Management tab, unchecked "Allow the computer to turn off this device to save power"
3. Applied the change, no restart required
4. Updated the NIC driver to the latest version from the manufacturer site
5. Monitored the machine for the rest of the day using continuous ping

No further drops were reported after the fix.

---

## Preventive Action

- Deploy a Group Policy that disables NIC power management across all domain workstations
- Include NIC driver updates in the standard OS patching and maintenance cycle
- Set up baseline network monitoring with continuous pings between workstations and the gateway to catch latency spikes before users notice
- Add NIC power management settings to the standard workstation build checklist

---

*[Back to README](../README.md)*
