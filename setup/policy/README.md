# Usage policy

`usagepolicy.json` is the CloudLabs usage policy for this lab. CloudLabs enforces it on every resource request in the attendee's resource group.

## What the lab uses in Azure

Modules 1 to 5 run in Power Apps, Power Automate, Microsoft Copilot Studio and Outlook. The Power Platform environment that Module 1 creates is not an Azure resource, so the usage policy does not govern it. Attendees create no Azure resources by hand.

The only Azure footprint is the lab VM that the Getting Started pages describe.

| Resource type | Limit | Why |
| --- | --- | --- |
| `Microsoft.Compute/virtualMachines` | 1 instance, 2 vCPUs | The lab VM. Sized for `Standard_D2s_v3`. |
| `Microsoft.Storage/storageAccounts` | 1 | Headroom for a diagnostics account if the template deploys one. Set it to `0` if the template has no storage account. |
| Cosmos DB, SQL Database, VM scale sets, Databricks, Synapse pools | 0 | Defensive zero-tail. The lab never uses these. |

## Before you register it

- If the CloudLabs template uses a VM size other than `Standard_D2s_v3`, set `max-cpu-cores` and `max-number-of-vCPUs` to that size's vCPU count. Otherwise the policy blocks the template's own VM.
- Upload the file to a publicly readable URL and set it as the template's **Usage Policy**. New permissions apply only to new deployments; for running ones, use **Manage Permissions** in the ODL control panel.
