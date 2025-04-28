<img width="600" src="https://github.com/user-attachments/assets/3139ed02-bf2c-4d30-973e-12dc1063fcba" alt="Incident Response Lifecycle"/>

# Incident Response Report: Potential Impossible Travel

## Platforms and Languages Leveraged
- Windows 10 Virtual Machines (Microsoft Azure)
- EDR Platform: Microsoft Defender for Endpoint
- Kusto Query Language (KQL)
- Microsoft Sentinel

##  Scenario

Management has raised concerns about potential unauthorized access to user accounts after receiving multiple "impossible travel" alerts. Sign-in logs for some accounts showed login attempts from geographically distant locations. Microsoft Entra ID( formerly known as Active Directory) flagged some of these attempts as suspicious due to the travel times between logins. At this stage, it is unclear whether any of the accounts have been compromised or if the activity results from user behavior. This investigation aims to detect any unauthorized access by reviewing login patterns, verifying user travel activity, and ensuring that accounts remain secure. Additionally, management is considering implementing geo-fencing and conditional access policies to mitigate future risks of unauthorized access.

### High-Level Incident Response Plan

- **Check `SigninLogs`** for any login attempts within a specific timeframe involving the same user account from geographically distant locations in an unreasonable timeframe, to identify potential unauthorized access.
- **Review `SigninLogs`** for each account to manually examine login timestamps and geolocations to assess if the time elapsed between different locations is reasonable.
- **If applicable, `disable affected accounts`, `reset credentials`, and `implement Conditional Access policies`** to prevent future unauthorized access attempts.

---

## Steps Taken

