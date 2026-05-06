# Network Setup Guide

A practical walkthrough for setting up a basic network from scratch. Whether it's a home setup or a small office, the steps are mostly the same. Connect the hardware, verify the configuration, and make sure everything can communicate with each other.

---

## Understanding the Key Components

Before plugging anything in, know what each device does:

- **Modem** - Brings the internet signal from your ISP into the building
- **Router** - Shares that connection across your network and assigns IP addresses via DHCP
- **Switch** - Expands the number of available wired ports on the network
- **Access Point (AP)** - Broadcasts the Wi-Fi signal to wireless devices

In most home or small office setups, the router handles all of these jobs in one box.

---

## Step 1 - Connect the Hardware

1. Plug the modem into the wall or ISP line
2. Connect the router to the modem using an Ethernet cable into the WAN port
3. Power on the modem first and wait for it to fully boot
4. Power on the router and wait for the status lights to stabilize
5. For wired devices, connect them to the router or switch using Ethernet cables

Give each device 60 to 90 seconds to fully boot before testing. Rushing this step just wastes time.

---

## Step 2 - Verify the IP Configuration

Once everything is connected, confirm that devices are getting valid IP addresses.

On a Windows machine:

```cmd
ipconfig /all
```

You should see:
- An IP address in the router range (e.g., 192.168.1.x)
- A subnet mask (e.g., 255.255.255.0)
- A default gateway matching the router IP (e.g., 192.168.1.1)
- DNS server entries

If you see 169.254.x.x, DHCP is not working. Check the cable and verify DHCP is enabled on the router.

---

## Step 3 - Test Connectivity

Test local network connectivity first:

```cmd
ping 192.168.1.1
```

Test internet routing without DNS:

```cmd
ping 8.8.8.8
```

Test DNS resolution:

```cmd
ping google.com
```

All three should succeed. If one fails, you know exactly which layer has the problem.

---

## Step 4 - Configure Wi-Fi

1. Open a browser and go to the router admin page, usually 192.168.1.1 or 192.168.0.1
2. Log in with the admin credentials (check the label on the router if unchanged)
3. Set a network name (SSID) and a strong Wi-Fi password
4. Set encryption to WPA2 or WPA3, never leave it open or on WEP

Always change the default router admin password. Default credentials are publicly known and are the first thing anyone tries when attacking a network.

---

## Step 5 - Basic Security Checklist

Before considering the setup complete, go through this list:

- [ ] Default router admin password changed
- [ ] Wi-Fi using WPA2 or WPA3 encryption
- [ ] Strong Wi-Fi password set
- [ ] WPS disabled
- [ ] Remote management disabled if not needed
- [ ] Router firmware updated to the latest version

---

## Common Setup Issues

**Device not getting an IP (shows 169.254.x.x)**
Check the cable, run `ipconfig /release` then `ipconfig /renew`, and verify DHCP is enabled on the router.

**Can ping 8.8.8.8 but cannot open websites**
This is a DNS issue. Check DNS settings with `ipconfig /all` or manually set DNS to 8.8.8.8.

**Wi-Fi connected but no internet**
Check if the router itself has internet by connecting via Ethernet and testing. If wired works but Wi-Fi does not, the issue is in the wireless configuration.

**Slow connection**
Check how many devices are actively using the network. Run a speed test via Ethernet to get a clean baseline reading.

---

*[Back to README](../README.md)*
