# Software Installation Guide

A practical reference for installing common software and dealing with the issues that come up during installation. Most installation problems have the same handful of causes and this guide covers all of them.

---

## Before Installing Anything

Run through this checklist first. It prevents most common errors:

- [ ] Is there enough disk space? Most software needs at least 1 to 5 GB free
- [ ] Is the internet connection stable? Interrupted downloads produce corrupt installers
- [ ] Do you have admin rights on the machine?
- [ ] Could the antivirus or firewall block the installer?

---

## Installing Common Software

### Microsoft Office

1. Go to microsoft.com/office and sign in with your Microsoft account
2. Click Install Office and download the installer
3. Run the installer, right-click and select Run as Administrator if prompted
4. Wait for the installation to complete, this usually takes 5 to 15 minutes
5. Open any Office app and sign in to activate the license

If activation fails, check that the license is tied to the correct Microsoft account. One license can only be active on a limited number of devices at the same time.

---

### Google Chrome

1. Go to google.com/chrome
2. Click Download Chrome and run the installer
3. Chrome installs automatically with no extra steps needed
4. Sign in with a Google account to sync bookmarks and settings

---

### Adobe Acrobat Reader

1. Go to get.adobe.com/reader
2. Uncheck any optional offers before downloading
3. Run the installer and follow the prompts
4. Set it as the default PDF viewer when prompted

---

## Troubleshooting Installation Errors

### Installer Won't Run or Closes Immediately

Most likely cause: missing admin rights or antivirus blocking the process.

Fix:
- Right-click the installer and select Run as Administrator
- Temporarily disable real-time protection in the antivirus
- Re-enable the antivirus immediately after installation finishes

---

### Installation Gets Stuck or Freezes

Most likely cause: corrupted download or not enough disk space.

Fix:
1. Cancel the installation
2. Delete the downloaded installer file
3. Check available disk space, you need at least twice the installer file size free
4. Re-download from the official source
5. Run again as Administrator

---

### Not Enough Disk Space Error

Fix:
1. Open File Explorer, right-click the C drive, select Properties
2. Click Disk Cleanup and remove temporary files
3. Check for large files or old downloads taking up space
4. If still not enough space, move files to an external drive before retrying

---

### Software Installed But Won't Open

Fix:
1. Restart the computer first, this clears most post-install issues
2. If it still won't open, uninstall it completely via Control Panel, Programs, Uninstall
3. Restart again, then reinstall from scratch
4. Check Windows Event Viewer for error logs if the problem continues

---

### Antivirus Keeps Blocking the Software

Fix:
- Add the software to the antivirus whitelist or exclusions list
- Only do this for software downloaded from the official source
- Never whitelist software from unknown or suspicious sources

---

## Uninstalling Software Properly

Never delete the program folder directly. Always uninstall through Windows:

1. Go to Control Panel, Programs, Uninstall a Program
2. Find the software, right-click, select Uninstall
3. Follow the uninstall wizard
4. Restart if prompted

For stubborn software that does not uninstall cleanly, use Revo Uninstaller to remove leftover files and registry entries.

---

*[Back to README](../README.md)*
