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
