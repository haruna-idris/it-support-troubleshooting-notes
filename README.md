# IT Support Troubleshooting Notes
Real world IT Support cases documented with solutions.
Each case includes: problem description, 
diagnosis, commands used, and resolution.

---

## Case 001 — WiFi Not Connecting After Restart
**Date:** May 12, 2026  
**OS:** Windows  
**Category:** Network Connectivity  
**Status:** ✅ Resolved  

---

### Problem Description
User reported that their computer was unable to 
connect to WiFi after a system restart. The built-in 
Windows troubleshooter failed to resolve the issue.

---

### Symptoms
- WiFi adapter showing but not connecting
- Windows troubleshooter not fixing the issue
- Issue persisted after manual restart

---

### Root Cause
Corrupted network stack configuration — common after 
Windows updates or improper shutdowns. The Winsock 
catalog and TCP/IP stack became corrupted preventing 
proper network adapter communication.

---

### Solution — Step by Step

**Step 1 — Open CMD as Administrator**
Press Windows + S, type cmd, 
right click → Run as Administrator

**Step 2 — Reset Network Stack**
```bash
netsh winsock reset
netsh int ip reset
ipconfig /release
ipconfig /flushdns
ipconfig /renew
```

**Step 3 — If issue persists after restart**
```bash
netcfg -d
```
Clears all network configurations completely.

**Step 4 — Restart the computer**
Allow Windows to rebuild network configuration 
on fresh boot.

---

### Commands Explained

| Command | What It Does |
|---|---|
| `netsh winsock reset` | Resets Winsock catalog to default |
| `netsh int ip reset` | Resets TCP/IP stack |
| `ipconfig /release` | Releases current IP address |
| `ipconfig /flushdns` | Clears DNS cache |
| `ipconfig /renew` | Requests new IP from DHCP |
| `netcfg -d` | Clears all network configurations |

---

### Resolution
Issue resolved after running network stack reset 
commands and restarting. WiFi connected successfully.

---

### Lessons Learned
- Always run winsock reset before netcfg -d
- Network stack corruption is common after updates
- ipconfig /flushdns often resolves DNS related 
  connectivity issues
- Document exact commands used for future reference

---

### Prevention
- Avoid force shutting down during Windows updates
- Keep network drivers updated via Device Manager
- Regular system maintenance prevents stack corruption

---

## Case Log
| Case | Issue | Date | Status |
|---|---|---|---|
| 001 | WiFi not connecting after restart | May 12, 2026 | ✅ Resolved |
