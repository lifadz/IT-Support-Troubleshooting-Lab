# Common Troubleshooting Reference

Quick reference for the most frequently reported issues in helpdesk environments. Each section follows the same logic. Check the obvious stuff first, then work deeper.

---

## 1. Computer Won't Turn On

Check first:
- Is the power cable plugged in at both ends?
- Is the power strip or outlet actually working? Test it with another device.
- Is the power button being pressed firmly?

If there is no response at all:
- Try a different power outlet
- On a desktop, check that the PSU switch on the back is set to I (on)
- Listen for any beeps when pressing the power button. Beep codes indicate hardware POST errors. Refer to the motherboard manual for the specific codes.

If it powers on but Windows will not load:
- Try booting with only essential hardware connected, remove USB drives and extra peripherals
- If the BIOS screen appears but Windows fails to start, run Startup Repair from the Windows recovery menu

CMOS reset (use this when BIOS settings are corrupted or causing boot issues):
1. Power off completely and unplug from the wall
2. Open the case and remove the coin-cell CMOS battery from the motherboard
3. Wait 5 minutes
4. Reinsert the battery, close the case, and power on
5. BIOS settings will reset to factory defaults

---

## 2. Slow Performance

Quick checks first:
1. Is the disk nearly full? Windows slows down significantly when the C drive is above 90% capacity
2. Open Task Manager with Ctrl + Shift + Esc and check CPU, RAM, and Disk usage
   - Disk usage at 90 to 100% on an HDD is a common cause of slowness
   - If RAM is maxed out, the machine may need a memory upgrade

Step-by-step fix:
1. Close unnecessary background applications
2. Disable startup programs via Task Manager, Startup tab. Disable anything that does not need to run at boot.
3. Run Disk Cleanup by right-clicking the C drive, selecting Properties, then Disk Cleanup
4. Run a malware scan. Malware often causes sustained high CPU usage.
5. Check for pending Windows updates since they sometimes run silently in the background

If the machine uses an older HDD, consider replacing it with an SSD. The performance difference is significant and it is one of the most cost-effective upgrades available.

---

## 3. Blue Screen of Death (BSOD)

A BSOD means Windows encountered an error it could not recover from. The error code on screen tells you where to look.

Immediate steps:
1. Note the error code displayed on the screen (e.g., IRQL_NOT_LESS_OR_EQUAL or MEMORY_MANAGEMENT)
2. Restart and see if it was a one-off. A single BSOD does not always mean a serious problem.
3. If it keeps happening, investigate further.

Common error codes and fixes:

| Error Code | Likely Cause | Fix |
|---|---|---|
| IRQL_NOT_LESS_OR_EQUAL | Driver issue | Update or roll back recent drivers |
| MEMORY_MANAGEMENT | RAM issue | Run Windows Memory Diagnostic |
| CRITICAL_PROCESS_DIED | Corrupted system file | Run sfc /scannow in CMD as admin |
| DRIVER_IRQL_NOT_LESS_OR_EQUAL | Faulty driver | Check recently installed or updated drivers |

Run System File Checker to repair corrupted Windows files:

```cmd
sfc /scannow
```

Run this in CMD as Administrator. It scans for and repairs corrupted system files automatically.

If the BSOD started after a recent change like a driver install or Windows update, use System Restore:
1. Type System Restore in the Start menu
2. Choose a restore point from before the issue started
3. Let it complete and test

---

## 4. Printer Not Printing

Check the basics:
- Is the printer powered on?
- Is the connection secure? Check the USB cable or confirm the network printer is on the same network.
- Is it set as the default printer in Windows?

Clear the print queue:
1. Go to Control Panel, Devices and Printers
2. Double-click the printer
3. Cancel all pending jobs in the queue

Restart the Print Spooler service:
1. Press Win + R, type `services.msc`, press Enter
2. Find Print Spooler in the list
3. Right-click and select Restart

If the printer still does not print:
- Remove the printer from Windows and re-add it
- Download the latest driver from the manufacturer website
- Run the Printer Troubleshooter via Settings, Devices, Printers and Scanners, select the printer, click Manage, then Run troubleshooter

---

## 5. Application Not Responding

Immediate fix:
1. Press Ctrl + Shift + Esc to open Task Manager
2. Find the application under Processes
3. Right-click and select End Task

If it keeps freezing:
- Check if the application has any pending updates and install them
- Check disk space since applications can freeze when the drive is nearly full
- Reinstall the application by uninstalling via Control Panel, restarting, then reinstalling fresh
- Check Windows Event Viewer for application error logs under Windows Logs, Application. Look for errors that match the time of the crash.

---

## 6. No Sound

Check first:
- Is the volume muted? Check the taskbar and any physical volume buttons.
- Is the correct playback device selected? Right-click the speaker icon in the taskbar and open Sound settings.

Fix:
1. Open Sound settings and confirm the correct output device is selected
2. If using external speakers or headphones, check the cable connection
3. Update the audio driver via Device Manager, Sound, video and game controllers
4. Run the Audio Troubleshooter via Settings, System, Sound, then Troubleshoot

---

*[Back to README](../README.md)*
