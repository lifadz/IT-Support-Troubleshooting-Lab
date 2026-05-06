# Security Best Practices

Security is not a one-time setup. It is a habit. Most breaches in small office environments happen because of basic things that were skipped or ignored. This guide covers the fundamentals that every IT Support engineer and end user should follow.

---

## 1. Password Hygiene

Weak passwords are still the most common entry point for attackers. It is low effort to fix and high impact.

Rules to follow:
- Minimum 12 characters, longer is better
- Mix uppercase, lowercase, numbers, and symbols
- Never reuse the same password across multiple accounts
- Never use obvious info like names, birthdays, company name, or anything predictable

Enable Two-Factor Authentication (2FA) on every account that supports it:
- Use an authenticator app like Google Authenticator or Authy
- Avoid SMS-based 2FA where possible since it can be intercepted
- Priority accounts are email, VPN, admin portals, and cloud services

Use a password manager:
- Tools like Bitwarden (free) or 1Password remove the excuse of having too many passwords to remember
- One strong master password protects everything else

---

## 2. Keep Everything Updated

Unpatched software is one of the most exploited attack vectors. Updates exist because vulnerabilities were found. Leaving them unpatched means leaving a known door open.

What to keep updated:
- Windows and the OS, enable automatic updates
- All installed applications
- Antivirus definitions
- Router and network device firmware
- Browser and browser extensions

For routers especially, check the admin panel periodically for firmware updates. Many people never update router firmware after the initial setup, which is a significant and unnecessary risk.

---

## 3. Antivirus and Endpoint Protection

You do not need to spend money on antivirus for basic protection. Windows Defender built into Windows 10 and 11 is genuinely effective when kept updated.

Minimum setup:
- Real-time protection: ON
- Cloud-based protection: ON
- Automatic sample submission: ON
- Scheduled full scan: weekly

What antivirus will not catch:
- Social engineering and phishing emails
- Users deliberately bypassing security warnings
- Insider threats

Security awareness training matters just as much as technical tools.

---

## 4. Data Backup

Ransomware encrypts files and demands payment. The only reliable defense is having a clean backup that was not connected when the attack happened.

3-2-1 Backup Rule:
- 3 copies of your data
- 2 different storage types (e.g., local drive and cloud)
- 1 copy stored offsite or kept offline

Keep at least one backup disconnected from the network when not in use. A backup that is always connected can also be encrypted by ransomware.

---

## 5. Least Privilege

Running daily tasks as a local admin means any malware that runs also has admin rights. That is unnecessary risk.

Best practice:
- Use a standard user account for daily work
- Use a separate admin account only when performing admin tasks
- On domain environments, follow the principle of least privilege, users only get access to what they actually need

---

## 6. Encrypt Sensitive Data

If a laptop gets stolen and the drive is encrypted, the data is safe. If it is not encrypted, everything on it is exposed immediately.

Enable encryption:
- Windows: BitLocker (built into Pro and Enterprise editions)
- macOS: FileVault (built in)
- External drives: use BitLocker To Go or VeraCrypt

Also use encrypted communication:
- HTTPS only, check for the padlock in the browser before entering any credentials
- Avoid sending sensitive data over unencrypted email

---

## 7. Secure the Network

Basic Wi-Fi security checklist:
- [ ] WPA2 or WPA3 encryption, never WEP or open
- [ ] Strong and unique Wi-Fi password
- [ ] Default router admin credentials changed
- [ ] WPS disabled
- [ ] Guest network set up separately for visitors and IoT devices
- [ ] Remote management disabled if not in use
- [ ] Router firmware up to date

---

## 8. Physical Security

Physical access bypasses most digital security controls. This part is often ignored.

- Lock your screen when stepping away, use Win + L on Windows
- Do not leave sensitive documents on your desk unattended
- Be aware of who can see your screen in shared or public spaces
- Shred documents with sensitive information before discarding them
- Never plug in a USB drive from an unknown source

---

*[Back to README](../README.md)*
