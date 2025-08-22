## Dashboard Panels

### Security Event Monitoring
- **Failed Login Attempts (EventCode 4625)** - Real-time counter of authentication failures
- **Failed Logons (Trend)** - Time-series visualization of failed authentication attempts
- **Failed Logons Over Time by Workstation** - Host-based analysis of security events
- **Failed Logons by Hour (Last 7 Days)** - Temporal pattern analysis for threat hunting

### User Account Security
- **Top Accounts with Failed Logons** - Identifies potentially targeted user accounts
- **Top Failure Reasons for Failed Logons (Last 30 Days)** - Root cause analysis of authentication issues

### Baseline Security Metrics
- **Successful Logons (4624) – Daily Trend** - Baseline authentication activity monitoring
- **Account Lockouts (4740) – Daily Trend** - Account security incident tracking

### Key Windows Event Codes Monitored
- **4624**: Successful logon events (baseline activity)
- **4625**: Failed logon attempts (security threats)
- **4740**: Account lockout events (security incidents)
