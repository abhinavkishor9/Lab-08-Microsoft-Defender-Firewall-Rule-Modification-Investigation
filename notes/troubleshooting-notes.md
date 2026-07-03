# Troubleshooting Notes

## Issue 1

Firewall logs not generating.

### Resolution

Verify the correct log location:

Applications and Services Logs

Microsoft

Windows

Windows Firewall With Advanced Security

Firewall

---

## Issue 2

Unable to locate Event ID 2003.

### Resolution

Ensure the firewall profile was actually modified.

Simply viewing firewall settings will not generate events.

---

## Issue 3

PowerShell still reports firewall enabled after changes.

### Resolution

Run PowerShell as Administrator.

Execute:

```powershell
Get-NetFirewallProfile
```

again after refreshing the firewall settings.

---

## Issue 4

Firewall toggle unavailable.

### Resolution

Check:

- Tamper Protection
- Group Policy restrictions
- Administrator privileges

---

## Issue 5

Firewall settings controlled by organization.

### Resolution

If the device is domain joined or managed by Group Policy, local configuration changes may be blocked.

Use a standalone Windows VM for lab exercises.

---

## Issue 6

Incorrect event log selected.

### Resolution

Do not investigate:

Windows Defender Operational logs

Instead use:

Applications and Services Logs

Microsoft

Windows

Windows Firewall With Advanced Security

Firewall

---

## Lessons Learned

- Firewall configuration changes are fully auditable.
- PowerShell provides quick verification of firewall status.
- Event ID 2003 records firewall configuration changes.
- Firewall modifications should always be validated against endpoint logs.
- Disabling the firewall can significantly reduce endpoint protection and should be investigated promptly.
