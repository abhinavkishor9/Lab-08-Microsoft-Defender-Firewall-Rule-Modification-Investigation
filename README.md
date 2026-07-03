# Lab-08-Microsoft-Defender-Firewall-Rule-Modification-Investigation
## Objective

Investigate Windows Defender Firewall configuration changes by enabling and disabling the Public Firewall profile, validating the configuration through PowerShell, and analyzing Windows Firewall Operational event logs.

This lab demonstrates how SOC analysts can detect unauthorized firewall modifications that may weaken endpoint security.

---

## Skills Learned

- Windows Defender Firewall administration
- Windows Event Viewer investigation
- Firewall Operational Logs
- PowerShell firewall verification
- Firewall configuration auditing
- Security monitoring
- Incident documentation
- SOC investigation workflow

---

## Tools Used

- Windows 10 VM
- Windows Defender Firewall
- Windows Security
- Event Viewer
- PowerShell

---

## MITRE ATT&CK Mapping

| Technique | Description |
|------------|-------------|
| T1562.004 | Impair Defenses: Disable or Modify System Firewall |
| T1562 | Impair Defenses |

---

# Lab Scenario

A SOC analyst receives an alert indicating that the Windows Defender Firewall configuration has changed on a workstation.

Firewall modifications are commonly performed by malware or attackers attempting to weaken endpoint protection before lateral movement or command-and-control communication.

The objective is to verify the firewall configuration, determine what changed, identify the corresponding Windows event logs, assess security impact, and document investigation findings.

---

# Lab Steps

## Step 1 — Review Current Firewall Configuration

Open PowerShell as Administrator.

Run:

```powershell
Get-NetFirewallProfile
```

Verify:

- Domain Profile
- Private Profile
- Public Profile

---

## Step 2 — Export Complete Firewall Configuration

Run:

```powershell
netsh advfirewall show allprofiles
```

Review:

- Firewall state
- Inbound policy
- Outbound policy
- Logging configuration
- Active profiles

---

## Step 3 — Disable Public Firewall

Navigate to:

**Windows Security → Firewall & network protection → Public Network**

Turn **Microsoft Defender Firewall** OFF.

Observe the warning indicating that the device is less protected.

---

## Step 4 — Enable Public Firewall

Turn the **Public Firewall** back ON.

Confirm the warning disappears and protection is restored.

---

## Step 5 — Verify Configuration Again

Run:

```powershell
Get-NetFirewallProfile
```

Confirm the Public profile is enabled again.

---

## Step 6 — Review Windows Firewall Event Logs

Open:

**Event Viewer → Applications and Services Logs → Microsoft → Windows → Windows Firewall With Advanced Security → Firewall**

Locate **Event ID 2003**.

Review:

- Firewall profile modified
- User
- Profile affected
- Configuration change
- Timestamp

---

# Investigation Summary

The Public Windows Defender Firewall profile was intentionally disabled and then re-enabled.

PowerShell verification confirmed firewall configuration before and after the modification.

Windows Firewall Operational logs generated **Event ID 2003** documenting the configuration change.

The investigation demonstrates how defenders can detect firewall modifications that could indicate attacker attempts to weaken endpoint protections.

---

# Outcome

- Successfully modified Windows Defender Firewall settings.
- Verified firewall configuration using PowerShell.
- Investigated Windows Firewall Operational logs.
- Correlated firewall configuration changes with Event ID 2003.
- Documented a complete SOC investigation workflow.
