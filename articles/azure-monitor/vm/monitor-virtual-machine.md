---
title: Monitor virtual machines with Azure Monitor
description: Learn how to use Azure Monitor to monitor the health and performance of virtual machines and their workloads.
ms.service: azure-monitor
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 06/02/2021

---

# Monitor virtual machines with Azure Monitor
This scenario describes how to use Azure Monitor to monitor the health and performance of virtual machines and their workloads. It includes collection of telemetry critical for monitoring, analysis and visualization of collected data to identify trends, and how to configure alerting to be proactively notified of critical issues.

> [!NOTE]
> This scenario describes how to implement complete monitoring of your Azure and hybrid virtual machine environment. To get started monitoring your first Azure virtual machine, see [Monitor Azure virtual machines](../../virtual-machines/monitor-vm.md). 

This article introduces the scenario and provides general concepts for monitoring virtual machines in Azure Monitor. If you want to jump right into a specific area, see one of the other articles that are part of this scenario described in the following table.

| Article | Description |
|:---|:---|
| [Enable monitoring](monitor-virtual-machine-configure.md) | Configure Azure Monitor to monitor virtual machines, which includes enabling VM insights and enabling each virtual machine for monitoring.  |
| [Analyze](monitor-virtual-machine-analyze.md) | Analyze monitoring data collected by Azure Monitor from virtual machines and their guest operating systems and applications to identify trends and critical information. |
| [Alerts](monitor-virtual-machine-alerts.md)   | Create alerts to proactively identify critical issues in your monitoring data. |
| [Monitor security](monitor-virtual-machine-security.md) | Discover Azure services for monitoring security of virtual machines. |
| [Monitor workloads](monitor-virtual-machine-workloads.md) | Monitor applications and other workloads running on your virtual machines. |

> [!IMPORTANT]
> This scenario doesn't include features that aren't generally available. Features in public preview such as [virtual machine guest health](vminsights-health-overview.md) have the potential to significantly modify the recommendations made here. The scenario will be updated as preview features move into general availability.

## Types of machines
This scenario includes monitoring of the following types of machines using Azure Monitor. Many of the processes described here are the same regardless of the type of machine. Considerations for different types of machines are clearly identified where appropriate. The types of machines include: 

- Azure virtual machines.
- Azure virtual machine scale sets.
- Hybrid machines, which are virtual machines running in other clouds, with a managed service provider, or on-premises. They also include physical machines running on-premises.

## Layers of monitoring
There are fundamentally four layers to a virtual machine that require monitoring. Each layer has a distinct set of telemetry and monitoring requirements. 

| Layer | Description |
|:---|:---|
| Virtual machine host | The host virtual machine in Azure. Azure Monitor has no access to the host in other clouds but must rely on information collected from the guest operating system. The host can be useful for tracking activity such as configuration changes, but typically isn't used for significant alerting. |
| Guest operating system | The operating system running on the virtual machine, which is some version of either Windows or Linux. A significant amount of monitoring data is available from the guest operating system, such as performance data and events. VM insights in Azure Monitor provides a significant amount of logic for monitoring the health and performance of the guest operating system. |
| Workloads | Workloads running in the guest operating system that support your business applications. Azure Monitor provides predefined monitoring for some workloads. You typically need to configure data collection and alerting for other workloads by using monitoring data that they generate. |
| Application | The business application that depends on your virtual machines can be monitored by using [Application Insights](../app/app-insights-overview.md). 

:::image type="content" source="media/monitor-virtual-machines/monitoring-layers.png" alt-text="Diagram that shows monitoring layers." lightbox="media/monitor-virtual-machines/monitoring-layers.png":::

## VM insights
This scenario focuses on [VM insights](../vm/vminsights-overview.md), which is the primary feature in Azure Monitor for monitoring virtual machines. VM insights provides the following features:

- Simplified onboarding of agents to enable monitoring of a virtual machine guest operating system and workloads. 
- Predefined trending performance charts and workbooks that you can use to analyze core performance metrics from the virtual machine's guest operating system.
- Dependency map that displays processes running on each virtual machine and the interconnected components with other machines and external sources.

## Agents
Any monitoring tool, such as Azure Monitor, requires an agent installed on a machine to collect data from its guest operating system. Azure Monitor currently has multiple agents that collect different data, send data to different locations, and support different features. VM insights manages the deployment and configuration of the agents that most customers will use. Different agents are described in the following table in case you require the particular scenarios that they support. For a detailed description and comparison of the different agents, see [Overview of Azure Monitor agents](../agents/agents-overview.md).

> [!NOTE]
> The Azure Monitor agent will completely replace the Log Analytics agent, diagnostic extension, and Telegraf agent once it gains required functionality. These other agents are still required for features such as VM insights, Microsoft Defender for Cloud, and Microsoft Sentinel.

- [Azure Monitor agent](../agents/agents-overview.md#azure-monitor-agent): Supports virtual machines in Azure, other cloud environments, and on-premises. Sends data to Azure Monitor Metrics and Logs. When it fully supports VM insights, Microsoft Defender for Cloud, and Microsoft Sentinel, then it will completely replace the Log Analytics agent and diagnostic extension.
- [Log Analytics agent](../agents/agents-overview.md#log-analytics-agent): Supports virtual machines in Azure, other cloud environments, and on-premises. Sends data to Azure Monitor Logs. Supports VM insights and monitoring solutions. This agent is the same agent used for System Center Operations Manager.
- [Dependency agent](../agents/agents-overview.md#dependency-agent): Collects data about the processes running on the virtual machine and their dependencies. Relies on the Log Analytics agent to transmit data into Azure and supports VM insights, Service Map, and Wire Data 2.0 solutions.
- [Azure Diagnostic extension](../agents/agents-overview.md#azure-diagnostics-extension): Available for Azure Monitor virtual machines only. Can send data to Azure Event Hubs and Azure Storage.

## Next steps

[Analyze monitoring data collected for virtual machines](monitor-virtual-machine-analyze.md)
