# Investigation Notes

## Incident Summary

Date:
03 July 2026

Analyst:
Abhinav Kishore

Lab:
Windows Defender Firewall Rule Modification Investigation

---

# Scenario

The SOC monitoring platform generated an alert indicating that the Windows Defender Firewall configuration had changed on an endpoint.

Firewall modifications are frequently observed during attacker activity because disabling or weakening firewall protections can allow malware, remote access tools, or lateral movement traffic to bypass endpoint security controls.

The objective of the investigation was to determine:

- Which firewall profile changed
- Whether the change was authorized
- Which user performed the action
- Whether Windows generated corresponding audit logs
- Overall security impact

---

# Investigation Timeline

## Initial Verification

Executed:

```powershell
Get-NetFirewallProfile
```

Observed:

- Domain Profile Enabled
- Private Profile Enabled
- Public Profile Enabled

---

## Configuration Review

Executed:

```powershell
netsh advfirewall show allprofiles
```

Reviewed:

- Firewall State
- Logging
- Policies
- Active Profiles

---

## Simulated Activity

Disabled:

Public Firewall

Observed Windows Security warning indicating endpoint protection was reduced.

---

## Configuration Restored

Re-enabled Public Firewall.

Verified configuration returned to its secure state.

---

## Event Log Investigation

Location:

Applications and Services Logs

Microsoft

Windows

Windows Firewall With Advanced Security

Firewall

Observed:

Event ID 2003

Description:

Windows Defender Firewall setting changed.

Fields reviewed:

- Firewall Profile
- User
- Application
- Timestamp

---

# Findings

Firewall profile modified:

Public

Action observed:

Disabled

Followed by:

Enabled

Windows generated Event ID 2003 confirming the configuration change.

PowerShell verification matched Event Viewer findings.

---

# Security Impact

Potential Impact:

- Reduced endpoint protection
- Increased exposure to inbound connections
- Potential malware communication
- Increased lateral movement opportunities

Severity:

Medium

Reason:

The firewall modification could weaken endpoint security but was restored immediately during the investigation.

---

# MITRE ATT&CK

T1562.004

Impair Defenses

Disable or Modify System Firewall

---

# SOC Analyst Conclusion

The investigation successfully demonstrated how firewall configuration changes can be validated using PowerShell and correlated with Windows Firewall Operational logs.

No malicious activity was identified during the exercise because the configuration change was intentionally performed for training purposes.
