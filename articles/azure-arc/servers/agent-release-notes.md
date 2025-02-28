---
title: What's new with Azure Arc-enabled servers agent
description: This article has release notes for Azure Arc-enabled servers agent. For many of the summarized issues, there are links to more details.
ms.topic: overview
ms.date: 04/18/2022
ms.custom: references_regions
---

# What's new with Azure Arc-enabled servers agent

The Azure Connected Machine agent receives improvements on an ongoing basis. To stay up to date with the most recent developments, this article provides you with information about:

- The latest releases
- Known issues
- Bug fixes

This page is updated monthly, so revisit it regularly. If you're looking for items older than six months, you can find them in [archive for What's new with Azure Arc-enabled servers agent](agent-release-notes-archive.md).

## Version 1.17 - April 2022

### New features

- The default resource name for AWS EC2 instances is now the instance ID instead of the hostname. To override this behavior, use the `--resource-name PreferredResourceName` parameter to specify your own resource name when connecting a server to Azure Arc.
- The network connectivity check during onboarding now verifies private endpoint configuration if you specify a private link scope. You can run the same check anytime by running [azcmagent check](manage-agent.md#check) with the new `--use-private-link` parameter.
- You can now disable the extension manager with the [local agent security controls](security-overview.md#local-agent-security-controls).

### Fixed

- If you attempt to run `azcmagent connect` on a server that is already connected to Azure, the resource ID is now printed to the console to help you locate the resource in Azure.
- The `azcmagent connect` timeout has been extended to 10 minutes.
- `azcmagent show` no longer prints the private link scope ID. You can check if the server is associated with an Azure Arc private link scope by reviewing the machine details in the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_HybridCompute/AzureArcCenterBlade/servers), [CLI](/cli/azure/connectedmachine?view=azure-cli-latest#az-connectedmachine-show), [PowerShell](/powershell/module/az.connectedmachine/get-azconnectedmachine), or [REST API](/rest/api/hybridcompute/machines/get).
- `azcmagent logs` collects only the 2 most recent logs for each service to reduce ZIP file size.
- `azcmagent logs` collects Guest Configuration logs again.

## Version 1.16 - March 2022

### Known issues

- `azcmagent logs` doesn't collect Guest Configuration logs in this release. You can locate the log directories in the [agent installation details](deployment-options.md#agent-installation-details).

### New features

- You can now granularly control which extensions are allowed to be deployed to your server and whether or not Guest Configuration should be enabled. See [local agent controls to enable or disable capabilities](security-overview.md#local-agent-security-controls) for more information.

### Fixed

- The "Arc" proxy bypass keyword no longer includes Azure Active Directory endpoints on Linux. Azure Storage endpoints for extension downloads are now included with the "Arc" keyword.

## Version 1.15 - February 2022

### Known issues

- The "Arc" proxy bypass feature on Linux includes some endpoints that belong to Azure Active Directory. As a result, if you only specify the "Arc" bypass rule, traffic destined for Azure Active Directory endpoints will not use the proxy server as expected. This issue will be fixed in an upcoming release.

### New features

- Network check improvements during onboarding:
  - Added TLS 1.2 check
  - Azure Arc network endpoints are now required, onboarding will abort if they are not accessible
  - New `--skip-network-check` flag to override the new network check behavior
  - On-demand network check now available using `azcmagent check`
- [Proxy bypass](manage-agent.md#proxy-bypass-for-private-endpoints) is now available for customers using private endpoints. This allows you to send Azure Active Directory and Azure Resource Manager traffic through a proxy server, but skip the proxy server for traffic that should stay on the local network to reach private endpoints.
- Oracle Linux 8 is now supported

### Fixed

- Improved reliability when disconnecting the agent from Azure
- Improved reliability when installing and uninstalling the agent on Active Directory Domain Controllers
- Extended the device login timeout to 5 minutes
- Removed resource constraints for Azure Monitor Agent to support high throughput scenarios

## Version 1.14 - January 2022

### Fixed

- A state corruption issue in the extension manager that could cause extension operations to get stuck in transient states has been fixed. Customers running agent version 1.13 are encouraged to upgrade to version 1.14 as soon as possible. If you continue to have issues with extensions after upgrading the agent, [submit a support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

## Version 1.13 - November 2021

### Known issues

- Extensions may get stuck in transient states (creating, deleting, updating) on Windows machines running the 1.13 agent in certain conditions. Microsoft recommends upgrading to agent version 1.14 as soon as possible to resolve this issue.

### Fixed

- Improved reliability when installing or upgrading the agent.

### New features

- Local configuration of agent settings now available using the [azcmagent config command](manage-agent.md#config).
- Proxy server settings can be [configured using agent-specific settings](manage-agent.md#update-or-remove-proxy-settings) instead of environment variables.
- Extension operations will execute faster using a new notification pipeline. You may need to adjust your firewall or proxy server rules to allow the new network addresses for this notification service (see [networking configuration](network-requirements.md)). The extension manager will fall back to the existing behavior of checking every 5 minutes when the notification service cannot be reached.
- Detection of the AWS account ID, instance ID, and region information for servers running in Amazon Web Services.

## Next steps

- Before evaluating or enabling Azure Arc-enabled servers across multiple hybrid machines, review [Connected Machine agent overview](agent-overview.md) to understand requirements, technical details about the agent, and deployment methods.
- Review the [Planning and deployment guide](plan-at-scale-deployment.md) to plan for deploying Azure Arc-enabled servers at any scale and implement centralized management and monitoring.
