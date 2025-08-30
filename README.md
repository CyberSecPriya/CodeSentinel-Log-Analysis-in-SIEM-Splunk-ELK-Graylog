# CodeSentinel Task3 - Log Analysis in SIEM (Splunk - TryHackMe Lab)

# Task Overview

This project was completed inside the TryHackMe SIEM Lab using Splunk with Sysmon logs.
The objective was to simulate a real-world security investigation by analyzing logs and identifying suspicious activity.

The main steps included:

1. Listing hosts and indexes sending logs

2. Finding the time range of available logs

3. Detecting abnormal spikes in activity

4. Building a timeline of suspicious host events

# Step 1: Hosts and Indexes

**Query Used:**

``index=windowslogs | stats count by index, host | sort -count``


**Explanation:**

This query lists the hosts that are sending logs into Splunk from the ``windowslogs`` index. In this case, we can see that the host ``cyber-host`` has contributed 12,256 events. This provides visibility into which machines are being monitored and helps narrow down targets for further investigation.

# Evidence - Hosts Sending Logs:

<img width="1897" height="585" alt="host ss1" src="https://github.com/user-attachments/assets/12c0ff30-a264-4a8f-8013-fc8e09cea7b7" />

# Step 2: Time Range of Logs

**Query Used:**

``index=windowslogs | stats earliest(_time) as first_log latest(_time) as last_log 
| convert ctime(first_log) ctime(last_log)``


**Explanation:**

This query identifies the earliest and latest log timestamps in the dataset. In this case, logs span from April 15, 2022 (first_log) to July 14, 2022 (last_log). Determining the log time range is crucial because it helps analysts understand the monitoring window and narrow down when suspicious activity or potential attacks may have occurred.

# Evidence:

<img width="1897" height="568" alt="log_time_range" src="https://github.com/user-attachments/assets/a5f567ec-fda7-4bd1-b9db-c92f99e5fbd8" />


# Step 3: Detecting Spikes / Suspicious Activity

**Query Used:**

``index=windowslogs | timechart count by host``

**Explanation:**

The timechart visualization highlights spikes in log activity across different hosts. Spikes often indicate unusual behavior such as brute-force attempts, privilege escalation, or malware beaconing. A host showing abnormal activity was chosen for deeper investigation.

# Evidence (Visualization):

<img width="1897" height="868" alt="Suspicious_Activity_Spike_Chart" src="https://github.com/user-attachments/assets/66d7c7cf-519b-4431-ae4b-db4090c71af9" />

# Step 4: Timeline of Suspicious Host

**Query Used:**

``index=windowslogs hostName | table _time host sourcetype source``

**Explanation:**

We extracted 12,245 events for the suspicious host. This timeline shows the chronological sequence of logs, helping to reconstruct what happened during the spike. Such analysis is useful to identify possible brute-force attempts or unusual system activity.

# Evidence (Table Output):

<img width="1898" height="862" alt="Suspicious_Host_Timeline" src="https://github.com/user-attachments/assets/5dc44e46-07c2-4016-8580-5ac227e1781a" />

# Conclusion

Through this log analysis exercise in the TryHackMe SIEM Lab (Splunk + Sysmon logs), I:

- Identified hosts and indexes generating logs

- Determined the dataset’s time range

- Detected abnormal spikes indicating suspicious activity

- Built a timeline of suspicious host activity

This investigation reflects real-world SIEM workflows and develops skills in threat detection, incident investigation, and security event correlation.

# Tools Used:

- Splunk (TryHackMe SIEM Lab), Sysmon Logs.

 # Note:
 
- This analysis was performed inside the TryHackMe SIEM Lab using Splunk with Sysmon logs.
 
- The dataset was provided for training purposes and may not reflect a full production environment.
 
- The goal of this project is to practice log analysis, attack investigation, and security event correlation in a controlled lab environment.  
