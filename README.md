<img width="600" src="https://github.com/user-attachments/assets/3139ed02-bf2c-4d30-973e-12dc1063fcba" alt="Incident Response Lifecycle"/>

# Incident Response Report: Potential Impossible Travel

## Platforms and Languages Leveraged
- Windows 10 Virtual Machines (Microsoft Azure)
- EDR Platform: Microsoft Defender for Endpoint
- Kusto Query Language (KQL)
- Microsoft Sentinel

##  Scenario

Management has raised concerns about potential unauthorized access to user accounts after receiving multiple "impossible travel" alerts. Sign-in logs for some accounts showed login attempts from geographically distant locations. Microsoft Entra ID( formerly known as Active Directory) flagged some of these attempts as suspicious due to the travel times between logins. At this stage, it is unclear whether any of the accounts have been compromised or if the activity results from typical user behavior. This investigation aims to detect any unauthorized access by reviewing login patterns, verifying user travel activity, and ensuring that accounts remain secure. Additionally, management is considering implementing geo-fencing and conditional access policies to mitigate future risks of unauthorized access.

### High-Level Incident Response Plan

- **Check `SigninLogs`** for any login attempts within a specific timeframe involving the same user account from geographically distant locations in an unreasonable timeframe, to identify potential unauthorized access.
- **Review `SigninLogs`** for each account to manually examine login timestamps and geolocations to assess if the time elapsed between different locations is reasonable.
- **If applicable, `disable affected accounts`, `reset credentials`, and `implement Conditional Access policies`** to prevent future unauthorized access attempts.

---

## Steps Taken

### 1. Searched Entra ID's `SigninLogs` Table

Searched for instances within the last 7 days where a user logged in from more than 2 different locations. Discovered 39 incidents where this behavior was exhibited

**Query used to locate events:**

![image](https://github.com/user-attachments/assets/ddc7576c-c25b-4bf1-acd8-dd0972895757)

---

### 2. Reviewed `SigninLogs` Table

Further investigated the accounts flagged with the highest number of instances. A total of four user accounts were identified: 

**Query used to locate events:**

![image](https://github.com/user-attachments/assets/653d3ad9-764d-4d90-b564-8a764d11a401)


Observed all 4 accounts, and nothing alarming stood out. Logins were consistent with the amount of time it takes to travel from one city to another. Also, no suspicious activity was found; logins occurred from expected locations and timeframes.

**Ex.: UserPrincipalName: 162e30755bc9a3e7dde8e...@....**

➡️From Quebec, Montreal to Windsor, Ontario:

<ul>
<li>Drive: ~ 9 hours</li>
<li>Flight: ~ 4 hours</li>
<li>Time Elapsed between logins: 1 day, 7 hours</li>
</ul>

![image](https://github.com/user-attachments/assets/0f1bdd26-63b8-4b9e-9294-b3789f7597e0)

---

### 3. No Remedial Action Was Taken

Since no unauthorized activity was detected, no device isolation, user disablement, or forced password resets were necessary. If suspicious or malicious activity had been detected, the following procedures would have been implemented: 

1) Disabling the affected Device in Entra ID:

   **Ex.**
   
![image](https://github.com/user-attachments/assets/58b6ec90-a4d1-496c-80d1-0a467a63121d)

2) Isolated the affected device and ran an antimalware scan
3) Blocked malicious devices

---

### 4. Evaluated Implementation of Conditional Access Policies and Closed Out Incident

Management explored the implementation of geo-fencing to restrict logins to specific geographical regions to better detect or block unexpected logins. Based on the team's analysis, the alerts were determined to be benign true positives due to legitimate travel or routine activity.

Reviewed and completed write-up for incident resolution. Finalized reporting and closed out the incident in Microsoft Sentinel as a true benign positive.

![image](https://github.com/user-attachments/assets/352dca63-6a5e-4a2d-bcfc-5e470765f243)









