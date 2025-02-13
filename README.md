
# Building a SOC + Honeynet in Azure (Live Traffic)
<img width="942" alt="image" src="https://github.com/user-attachments/assets/002968e2-9cae-483e-9fff-db4451599125" />


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<img width="890" alt="image" src="https://github.com/user-attachments/assets/ded03a25-5b68-40d1-bb2f-6813754f3a09" />


## Architecture After Hardening / Security Controls
<img width="834" alt="image" src="https://github.com/user-attachments/assets/a3a112e8-e299-4a33-bb95-c00a18fc1280" />


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
<img width="946" alt="image" src="https://github.com/user-attachments/assets/d30c9250-590c-4e56-ac2d-8eef155b6f94" />

<img width="934" alt="image" src="https://github.com/user-attachments/assets/fc0e3386-9d7b-4443-8e87-0eb3c919eebf" />

<img width="898" alt="image" src="https://github.com/user-attachments/assets/1703242c-a539-4b07-a39d-a85ae61a8833" />

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2025-01-04T14:26:10.7900377Z
Stop Time 2025-01-05T14:26:10.7900377Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 78464
| Syslog                   | 6854
| SecurityAlert            | 20
| SecurityIncident         | 244
| AzureNetworkAnalytics_CL | 2644

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2025-01-05T21:30:47.2782052Z
Stop Time	2025-01-06T21:30:47.2782052Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 5774
| Syslog                   | 29
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
