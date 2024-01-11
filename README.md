# Active Directory Performance Assessment workbook (v4)
## Overview
Do you know how to monitor **_custom_** performance counters by using Log Analytics and the Azure Monitor workbooks?
In this case, I will use the Active Directory Domain Controllers as example. Below, you will be able to find an Azure Workbook to assess the essential Active Directory performance counters.
 
You have likely heard or read about [VM Insights](https://learn.microsoft.com/en-us/azure/azure-monitor/vm/vminsights-overview) as a quick and easy method for getting started monitoring the client workloads on your virtual machines, especially if you are looking for a solution to manage OS Performance Counters. This solution is available for Azure Virtual Machines and Virtual Machines out of Azure through Azure ARC agent for both Linux and Windows. That is interesting and, many times, the easiest way to do it.

But, what happens if you want to collect and start monitoring **_custom_** Performance Counters? Here, a good option is to use [Data Collection Rules (DCRs)](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-rule-overview) to collect that custom information and then use [Azure Monitor Workbooks](https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-overview) for visualization or [Azure Alerts (log alerts)](https://learn.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-overview) to notify and alert.

I want to share the Active Directory Performance Assessment workbook, which I have been working on and will help you to monitor your Active Directory environment. You can use this as an example of a custom Azure Workbook to visualize Performance Counters. Specifically, you are going to find tiles, graphs, and dashboards for Operating System and Active Directory performance counters listed on **_Materials/List_of_Performance_Counters.txt_** file.

To use this workbook, you only need to follow these steps:
1. Use the [**Azure Monitor Agent**](https://learn.microsoft.com/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal) to connect your Domain Controllers to Log Analytics.
2. Create a [**Data Collection Rule**](https://learn.microsoft.com/en-us/azure/azure-monitor/essentials/data-collection-rule-overview?tabs=portal) to collect the performance counters and associate it to your Domain Controllers. (You will find the _DCR-ADPAS-PerformanceCounters-TEMPLATE.json_ file to do that in the **_Materials_** folder).
3. Deploy the **Active Directory Performance Assessment Workbook** you will find in the **_Materials_** folder.

## Workbook Summary
ADPA with Azure Monitor workbook
The Azure Workbook is divided into four sections (Availability, Operating System, Active Directory, and Detailed).

![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/eb823dfc-eeee-4e3f-baf6-e42370f1aa23)

**Availability**

This view summarizes how the servers send heartbeats to the Log Analytics workspace. It shows data from the last hour and the last _TimeRange_ parameter days.

![image](https://github.com/dmrellan/Active-Directory-Performance-Assessment-with-Azure-Monitor-workbook/assets/35997289/9e9ccf40-7da5-4b1e-8690-82121d8f7dc0)


**Operating System**

This section allows you to analyze the evolution of Operating System Performance Counters (Processor, Memory, LogicalDisk, Network).
Computer filter is available to select the servers to show.
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

----
**Version History**

_v4_ (11/01/2024)
- Workbook: Typos and links improved. Added Top tables to Operating System tab.
- Data Collection Rule _template_ provided.
