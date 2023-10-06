# Active Directory Performance Assessment with Azure Monitor workbook
- [Overview](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/edit/main/README.md#overview)
- [Workbook Summary](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/edit/main/README.md#workbook-summary)

## Overview
Today, I am here to talk to you about monitoring your custom performance counters using the Azure Monitor workbook. I will use the Active Directory Domain Controllers as an example in this case. Here, you will find the analysis of the most essential Perf Counters to assess an Active Directory environment.
 
Likely, you have heard or read about [VM Insights](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-overview) as a solution to provide a quick and easy method for getting started monitoring the client workloads on your virtual machines, especially if you are looking for a solution to manage OS Performance Counters. As you can read in the official doc, this solution is available for Azure Virtual Machines and Virtual Machines out of Azure through Azure ARC agent for both Linux and Windows. That is interesting and, many times, the easiest way to do it.
 
But what happens if you want to collect and start monitoring custom Performance Counters? Here, a good option is to use [Data Collection Rules (DCRs)](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-rule-overview) to collect that custom information and then use [Azure Monitor Workbooks](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-overview) to visualize or [Azure Alerts (log alerts)](https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-overview) to notify and alert.
 
Below, I want to share the Active Directory Performance Assessment with Azure Monitor workbook in which I have been working on, and it is helpful in an Active Directory context. You can use this as an example of a custom Azure Workbook to visualize Performance Counters. Specifically, you will see tiles, graphs, and dashboards for the following performance counters.

	• Database(lsass)\Database Cache % Hit
	• Database(lsass)\Database Cache Size (MB)
	• Database(lsass)\Database Cache Size Effective (MB)
	• DirectoryServices(NTDS)\DRA Pending Replication Operations
	• DirectoryServices(NTDS)\DRA Pending Replication Synchronizations
	• DirectoryServices(NTDS)\LDAP Client Sessions
	• LogicalDisk(*)\% Idle Time
	• LogicalDisk(*)\Avg. Disk Queue Length
	• LogicalDisk(*)\Avg. Disk Read Queue Length
	• LogicalDisk(*)\Avg. Disk sec/Read
	• LogicalDisk(*)\Avg. Disk sec/Write
	• LogicalDisk(*)\Avg. Disk Write Queue Length
	• LogicalDisk(*)\Free Megabytes
	• Memory(*)\Available MBytes
	• Memory(*)\Free System Page Table Entries
	• Memory(*)\Pages/sec
	• Memory(*)\Pool Nonpaged Bytes
	• Memory(*)\Pool Paged Bytes
	• Memory(*)\System Cache Resident Bytes
	• Netlogon(*)\Average Semaphore Hold Time
	• Netlogon(*)\Semaphore Acquires
	• Netlogon(*)\Semaphore Timeouts
	• Network Interface(*)\Output Queue Length
	• NTDS(*)\ATQ Estimated Queue Delay
	• NTDS(*)\ATQ Outstanding Queued Requests
	• NTDS(*)\ATQ Request Latency
	• NTDS(*)\ATQ Threads LDAP
	• NTDS(*)\ATQ Threads Other
	• NTDS(*)\ATQ Threads Total
	• NTDS(*)\LDAP Active Threads
	• NTDS(*)\LDAP Bind Time
	• NTDS(*)\LDAP Searches/sec
	• NTDS(*)\LDAP Successful Binds/sec
	• NTDS(*)\LDAP Writes/sec
	• NTDS(*)\NTLM Binds/sec
	• Paging File(*)\% Usage
	• Process(_Total)\% Processor Time
	• Process(dfsrs)\% Processor Time
	• Process(dfsrs)\Handle Count
	• Process(dfsrs)\Private Bytes
	• Process(dfsrs)\Working Set
	• Process(dns)\% Processor Time
	• Process(dns)\Handle Count
	• Process(dns)\Private Bytes
	• Process(dns)\Working Set
	• Process(lsass)\% Processor Time
	• Process(lsass)\Handle Count
	• Process(lsass)\Private Bytes
	• Process(lsass)\Working Set
	• Processor Information(_Total)\Average Idle Time
	• Processor(_Total)\% C1 Time
	• Processor(_Total)\% C2 Time
	• Processor(_Total)\% C3 Time
	• Processor(_Total)\% DPC Time
	• Processor(_Total)\% Idle Time
	• Processor(_Total)\% Privileged Time
	• Processor(_Total)\% Processor Time
	• Processor(["_Total"])\% User Time
	• Processor(["_Total"])\DPC Rate
	• Processor(["_Total"])\DPCs Queued/sec
	• Security System-Wide Statistics(*)\Kerberos Authentications
	• Security System-Wide Statistics(*)\NTLM Authentications
	• TCPv4([""])\Connection Failures

To use this workbook, you only need to following these steps:
- 1 - To connect your Domain Controllers to report to Log Analytics (Azure ARC agent + Azure Monitor Agent extension if DCs resides on-premises)
- 2 - Create a DCR to collect the above performance counters (Sample rate for each of counters = 60 seconds).
- 3 - Deploy the Azure Workbook.

## Workbook Summary
ADPAS with Azure Monitor workbook
The Azure Workbook is divided into four sections (Availability, Operating System, Active Directory, and Detailed).

![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/eb823dfc-eeee-4e3f-baf6-e42370f1aa23)

**Availability**

This view summarizes how the servers send heartbeats to the Log Analytics (heartbeats). It shows data from the last hour and the last 30 days.
![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/9e9ccf40-7da5-4b1e-8690-82121d8f7dc0)


**Operating System**

This section allows us to analyze the evolution of Operating System Performance Counters (Processor, Memory, LogicalDisk, Network).
A computer filter is available to select the servers to show.
There are two graphs per counter:
	• Left: Counter evolution.
	• Right: Detailed table per instance: Status (if it applies), name, average, standard deviation, and percentiles (50, 75, and 95) in the selected TimeRange.
![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/a74f71d8-87b1-4981-87b2-0b079e87c649)

**Active Directory**

Active Directory tab analyzes the evolution of Active Directory Performance Counters (Authentications, Directory Services, lsass, DNS, DFSRS, and NTDS).
A computer filter is available to select the servers to show.
You can find the same graphs that OS tab has per counter: Evolution and detailed table.
![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/4d51dbf3-7270-4ac8-9476-55011d16fff0)

**Detailed**

It allows the detailed analysis of the selected counter and computer. Customized granularity can be selected.
![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/1441c74e-3db7-489a-b09b-83e806799877)
