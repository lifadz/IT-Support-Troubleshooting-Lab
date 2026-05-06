# How to Block Websites on Windows

Sometimes you need to block access to specific websites on a machine, whether it is restricting distracting sites on a shared workstation or preventing access to unauthorized content on a company device. This guide covers two practical methods.

---

## Method 1 - Using the Windows Hosts File

The hosts file is a local text file that Windows checks before sending out a DNS request. By pointing a domain to 127.0.0.1 (the local machine itself), you effectively block it. The browser tries to load it locally, gets nothing, and the site fails to open.

This works on any Windows machine with no extra tools required.

### Steps

**1. Open Notepad as Administrator**

Press Win + S and search for Notepad. Right-click Notepad and select Run as administrator. Click Yes on the UAC prompt.

You must run as administrator. The hosts file is a protected system file and cannot be saved without admin rights.

**2. Open the Hosts File**

In Notepad, go to File then Open and navigate to:

```
C:\Windows\System32\drivers\etc\
```

Change the file type filter from Text Documents to All Files. Otherwise the hosts file will not appear in the folder.

Open the file named `hosts` with no file extension.

**3. Add the Domains to Block**

Scroll to the bottom of the file and add a new line for each domain you want to block:

```
127.0.0.1   www.facebook.com
127.0.0.1   facebook.com
127.0.0.1   www.youtube.com
127.0.0.1   youtube.com
```

Always block both www.domain.com and domain.com since some browsers try both versions.

**4. Save the File**

Press Ctrl + S to save. If Windows asks to confirm, click Yes.

**5. Flush the DNS Cache**

Open CMD and run:

```cmd
ipconfig /flushdns
```

This clears any cached DNS entries so the block takes effect immediately without needing a reboot.

**6. Test It**

Open a browser and try to visit the blocked site. It should fail to load or show a connection error.

### Removing a Block

Open the hosts file again as Administrator, delete the lines you added, save the file, then flush DNS again:

```cmd
ipconfig /flushdns
```

---

## Method 2 - Using the Router

If you need to block a site for everyone on the network and not just one machine, do it at the router level instead.

Steps:
1. Log into the router admin page, usually 192.168.1.1 or 192.168.0.1
2. Look for a section called Parental Controls, Access Control, or URL Filtering (the name varies by router brand)
3. Add the domains you want to block
4. Save and apply

Router-level blocking is more effective than the hosts file method because it applies to every device on the network and cannot be bypassed by editing the hosts file on individual machines.

---

## Important Notes

- The hosts file method only applies to the machine where it is configured
- A user with local admin rights can undo it by editing the hosts file themselves
- For a managed environment, enforce website blocking via Group Policy or a DNS filtering solution like Cisco Umbrella or Cloudflare Gateway for more reliable and scalable control

---

*[Back to README](../README.md)*
