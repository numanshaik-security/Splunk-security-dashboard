🔐 Windows Security Monitoring with Splunk

This project is a hands-on SIEM (Security Information and Event Management) dashboard built in Splunk to monitor Windows Security, System, and Application logs.

It provides real-time visibility into:

Failed logons (4625) → detect brute-force or suspicious login attempts

Successful logons (4624) → establish a baseline of normal activity

Account lockouts (4740) → highlight potential security incidents

Failure reasons, top accounts, and hourly trends → speed up triage and root cause analysis

The dashboard panels are designed to answer:

What is happening right now?

Who is being targeted?

When do spikes occur?

Where are failed attempts coming from?

This repo includes screenshots, SPL queries, and lessons learned — making it a portfolio-ready showcase of applied SIEM and detection engineering skills.

## 📊 Dashboard Screenshots

### Failed Login Attempts (EventCode 4625)
![Failed Login Attempts](Failed_Login_Attempts_Overview.png)

### Failed Logons Trend
![Failed Logons Trend](Failed_Logons_Trend_Chart.png)

### Top Accounts with Failed Logons
![Top Accounts](Top_Failed_Login_Accounts.png)

### Failed Logons Over Time by Workstation
![Workstation Trend](Failed_Logons_by_Workstation_Timeline.png)

### Failed Logons by Hour (Last 7 Days)
![Hourly Failed Logons](Hourly_Failed_Logons_7Days.png)

### Top Failure Reasons (Last 30 Days)
![Failure Reasons](Top_Login_Failure_Reasons_30Days.png)

### Successful Logons (4624) – Daily Trend
![Successful Logons](Successful_Logons_Daily_Trend.png)

### Account Lockouts (4740) – Daily Trend
![Account Lockouts](Account_Lockouts_Daily_Trend.png)
-------------------------------------------------------------------------------------------------
## 🔍 SPL Queries 

### 1) Failed Login Attempts (EventCode 4625) — Daily Count
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4625
| timechart span=1d count AS Failed_Logons
```
### 2) Failed Logons (Trend) — Hourly
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4625
| timechart span=1h count AS Failed_Logons
```
### 3) Top Accounts with Failed Logons (Last 30 Days)
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4625 earliest=-30d
| stats count AS Failed_Count by Account_Name
| sort - Failed_Count
| head 10
```
### 4) Failed Logons Over Time by Workstation
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4625
| fillnull value="(unknown)" Workstation_Name
| timechart span=1h count BY Workstation_Name
```
### 5) Failed Logons by Hour (Last 7 Days)
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4625 earliest=-7d
| eval hour=strftime(_time,"%H")
| stats count AS Failed_Count by hour
| sort hour
```
### 6) Top Failure Reasons for Failed Logons (Last 30 Days)
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4625 earliest=-30d
| fillnull value="(unspecified)" Failure_Reason
| stats count AS Failed_Count by Failure_Reason
| sort - Failed_Count
| head 10
```
### 7) Successful Logons (4624) — Daily Trend
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4624
| timechart span=1d count AS Successful_Logons
```
### 8) Account Lockouts (4740) — Daily Trend
```spl
index=winlogs sourcetype=WinEventLog:Security EventCode=4740
| timechart span=1d count AS Account_Lockouts
```
📘 Lessons Learned

I wanted to get hands-on with a SIEM, so I built a Windows security dashboard in Splunk. Along the way I learned:

How to ingest Windows Event Logs (Security, System, Application) and map the fields that matter.

What key event codes mean in practice: 4625 (failed logon), 4624 (successful logon), 4740 (account lockout).

How to write SPL for trends, top-N breakdowns, and hourly patterns that actually help with triage.

How to organize a dashboard so it tells a story: what’s happening, who’s impacted, when it spikes.

I hit a snag with email alerts (scheduler/SMTP). I documented the search logic and left alerting as a follow-up—it’s realistic and I know what to fix next.

Bonus: I’m now much more comfortable using GitHub for documentation and sharing work.

🚀 Future Improvements

Finish the brute-force alert (>=5 failed logons in 5m) with SMTP configured.

Add a Sysmon panel (process creation and network connections) for deeper host visibility.

Correlate 4740 lockouts with the preceding 4625 failures to pinpoint the source workstation.

Add a sample dataset so others can reproduce the visuals without a Windows host.

Export and include a prebuilt dashboard JSON/XML (done) and a small setup script for faster onboarding.
