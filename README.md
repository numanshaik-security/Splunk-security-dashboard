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
