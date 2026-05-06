# Hardware Maintenance Guide

Hardware does not maintain itself. A little regular upkeep goes a long way. It prevents unexpected failures, extends component life, and keeps systems running at full performance. This guide covers the basics every IT Support engineer should know.

---

## 1. Physical Cleaning

Dust is the number one silent killer of hardware. It clogs fans, insulates heat sinks, and causes components to overheat over time.

How often: Every 3 to 6 months, or sooner in dusty environments.

Steps:
1. Power off the machine completely and unplug all cables
2. Move it to a ventilated area since compressed air blows dust everywhere
3. Open the case
4. Use compressed air to blow out dust from the CPU heatsink and fan, GPU heatsink and fans, case fans, power supply vents, RAM slots, and expansion slots
5. Use a microfiber cloth to wipe down the exterior, monitor, and peripherals
6. Never use a vacuum cleaner directly on components since static discharge can damage them

If a fan sounds louder than usual or is grinding, it is already overdue for a clean or needs to be replaced.

---

## 2. Monitor System Temperatures

Overheating causes throttling, random crashes, and shortened component lifespan. Know what normal temperatures look like for each machine.

Tools to use:
- HWMonitor - detailed readings for CPU, GPU, and drives
- Core Temp - focused on CPU temperature
- CrystalDiskInfo - monitors hard drive health and temperature

Safe temperature ranges (approximate):

| Component | Normal | Warning |
|---|---|---|
| CPU (idle) | 30 to 50°C | Above 80°C under load |
| GPU (under load) | 60 to 85°C | Above 95°C |
| Hard Drive | 30 to 50°C | Above 60°C |

If temperatures are consistently high, check the fans and clean out dust before doing anything else.

---

## 3. Keep Drivers Updated

Outdated drivers cause crashes, performance issues, and compatibility problems, especially after Windows updates.

Key drivers to keep current:
- GPU driver (Intel, AMD, or NVIDIA)
- Network adapter driver
- Chipset and motherboard driver
- Storage controller driver

How to update:
1. Open Device Manager
2. Right-click the device, select Update driver, then Search automatically
3. Or go directly to the manufacturer website for the latest version

For graphics cards, always get drivers from the manufacturer website directly. Manufacturer drivers are more current and stable than what Windows Update provides.

---

## 4. Hard Drive Health Checks

Storage failure can mean data loss. Catching a failing drive early matters.

Run a health check monthly using CrystalDiskInfo. Look for the health status:
- Good is normal
- Caution means the drive is showing early warning signs

Pay attention to reallocated sectors and pending sectors. These indicate physical damage and the drive should be replaced soon.

For HDDs, run defragmentation periodically:
1. Open Defragment and Optimize Drives from the Start menu
2. Select the HDD and click Optimize

Do not defragment SSDs. It is unnecessary and reduces their lifespan.

---

## 5. RAM Check

Random crashes, BSODs, and freezes that seem unrelated are often RAM issues.

How to run Windows Memory Diagnostic:
1. Press Win + R, type `mdsched`, press Enter
2. Select Restart now and check for problems
3. The tool runs automatically on the next boot and reports any errors

If errors are found, test each RAM stick individually by removing all but one to identify the faulty module.

---

## 6. Regular Backups

Hardware always fails eventually. The question is whether the data survives it.

Backup strategy:
- Local backup: copy important files to an external drive regularly
- Cloud backup: use Google Drive or OneDrive for critical documents
- System image: use Macrium Reflect (free) to create a full image of the OS drive

If the drive fails or Windows breaks, a system image lets you restore everything in minutes.

Recommended backup frequency:

| Data Type | Frequency |
|---|---|
| Critical work files | Daily or real-time via cloud sync |
| Full system image | Weekly or before major changes |
| External drive backup | Weekly |

---

*[Back to README](../README.md)*
