# Case 03 - DNS Resolution Failure: Websites Won't Load by Name

## Scenario

A user reports they cannot open any websites. Their machine has a valid IP address, gateway, and DNS entries in ipconfig. The network icon shows no issues. Ten minutes later, another user reports the same problem. The issue is affecting multiple people at the same time.

---

## Symptoms

- Browser shows DNS_PROBE_FINISHED_NXDOMAIN or "Server not found"
- Websites cannot be accessed by name (e.g., www.google.com)
- `ping google.com` fails with "could not find host"
- `ping 8.8.8.8` succeeds, meaning internet routing is working fine
- Multiple users on the same network are affected simultaneously

---

## Troubleshooting Steps

**Step 1 - Confirm that IP pings work but name pings fail**

```cmd
ping 8.8.8.8
```
This should succeed and confirms that internet routing is working.

```cmd
ping google.com
```
This should fail and confirms that DNS resolution is broken.

This is the key test that separates a DNS issue from a full connectivity failure.

---

**Step 2 - Check DNS settings with ipconfig /all**

```cmd
ipconfig /all
```

Look at the DNS Servers field:
- Blank means DNS was never configured or was wiped
- Wrong IP means DNS is misconfigured and pointing to the wrong server

---

**Step 3 - Test DNS resolution with nslookup**

```cmd
nslookup google.com
```

- "DNS request timed out" means the DNS server is not responding
- "Non-existent domain" means the server is up but cannot resolve the name

Try querying a different DNS server directly to narrow it down:

```cmd
nslookup google.com 8.8.8.8
```

If this works, the local or internal DNS server is the problem. If this also fails, check whether a firewall is blocking UDP port 53.

---

**Step 4 - Flush the local DNS cache**

```cmd
ipconfig /flushdns
```

If this fixes the issue, the local cache had corrupted or stale entries.

---

**Step 5 - Check if the DNS server is reachable**

```cmd
ping <DNS_server_IP>
```

If the DNS server does not respond to ping, it may be down or unreachable on the network.

---

**Step 6 - Temporarily switch to a public DNS server**

To restore access for users while investigating the root cause:
1. Go to Network Adapter, Properties, IPv4
2. Set Primary DNS to 8.8.8.8 and Secondary DNS to 8.8.4.4

If browsing restores immediately, the internal DNS server is confirmed as the problem.

---

**Step 7 - Check the internal DNS server**

- Verify the DNS service is running in services.msc
- Check DNS server event logs for errors
- Verify DNS forwarders are configured correctly
- Check server resource usage including CPU, memory, and disk

---

## Root Cause

The internal DNS server running on Windows Server had encountered a memory issue and the DNS service had stopped automatically. The server itself was still pingable, which is why basic monitoring did not catch it right away. Since the DHCP server was pointing all clients to this internal DNS, every user on the network was affected at the same time.

---

## Solution

1. Connected to the DNS server remotely via RDP
2. Opened services.msc and confirmed the DNS Server service was stopped
3. Started the DNS Server service
4. Tested resolution:

```cmd
nslookup google.com
```

Resolution was restored within seconds. All affected users were notified and the temporary DNS change was reverted back to the internal server.

---

## Preventive Action

- Set up a secondary DNS server so resolution continues if the primary fails
- Configure monitoring and alerting on the DNS service so the team is notified immediately if it stops
- Always push at least two DNS servers via DHCP, one internal and one public as a fallback
- Schedule regular server health checks and set memory usage alerts

---

*[Back to README](../README.md)*
