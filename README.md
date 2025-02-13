
# Building a SOC + Honeynet in Azure (Live Traffic)
<img width="942" alt="image" src="https://github.com/user-attachments/assets/002968e2-9cae-483e-9fff-db4451599125" />


## Introduction

In this project, I set up a mini honeynet in Azure, simulating a vulnerable environment to monitor and analyze potential threats. Logs from various sources were ingested into a Log Analytics workspace, which was then integrated with Microsoft Sentinel to generate attack maps, trigger alerts, and create incidents.

To assess the impact of security controls, I:

✅ Collected baseline security metrics from the insecure environment over a 24-hour period.

✅ Applied security hardening measures to improve the system’s defense.

✅ Measured the post-hardening metrics for another 24 hours to compare results.

Key Security Metrics Monitored:

📌 SecurityEvent – Windows event logs

📌 Syslog – Linux event logs

📌 SecurityAlert – Alerts triggered in Log Analytics

📌 SecurityIncident – Incidents detected by Microsoft Sentinel

📌 AzureNetworkAnalytics_CL – Malicious network traffic detected

This project demonstrates how proactive security measures can significantly reduce attack exposure and enhance threat visibility in a cloud environment.

## Architecture Before Hardening / Security Controls
<img width="890" alt="image" src="https://github.com/user-attachments/assets/ded03a25-5b68-40d1-bb2f-6813754f3a09" />


## Architecture After Hardening / Security Controls
<img width="834" alt="image" src="https://github.com/user-attachments/assets/a3a112e8-e299-4a33-bb95-c00a18fc1280" />


The mini honeynet in Azure was designed with the following key components:

🔹 Virtual Network (VNet) – Provides network segmentation.

🔹 Network Security Group (NSG) – Controls inbound/outbound traffic.

🔹 Virtual Machines – (2 Windows, 1 Linux) act as monitored endpoints.

🔹 Log Analytics Workspace – Collects and analyzes security logs.

🔹 Azure Key Vault – Secures sensitive credentials.

🔹 Azure Storage Account – Stores log data.

🔹 Microsoft Sentinel – Functions as the SIEM, detecting and responding to threats.

Security Posture: Before vs. After Hardening

🛑 BEFORE:

- All resources were fully exposed to the internet.
- Virtual Machines had open NSGs and firewalls disabled.
- Public endpoints were accessible without Private Endpoints or restrictions.

✅ AFTER:

- NSGs hardened to block all traffic except from a secured admin workstation.
- Virtual Machines were secured using built-in firewalls and Private Endpoints.
- All resources were removed from public exposure, reducing the attack surface.
- This transformation highlights the impact of security hardening on cloud environments by minimizing exposure and improving threat resilience. 

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

In this project, a mini honeynet was successfully deployed in Microsoft Azure, with log sources integrated into a Log Analytics workspace. Microsoft Sentinel was utilized to monitor the environment, triggering alerts and generating incidents based on ingested security logs.

To assess the effectiveness of security controls, key metrics were measured:

- Before hardening – Resources were fully exposed, resulting in a high volume of security events and incidents.
- After implementing security controls – The number of security alerts and incidents significantly decreased, demonstrating the impact of a well-configured security posture.

It is important to note that in a real-world scenario with active user traffic, more security events and alerts may have been generated even after hardening the environment. However, this project highlights how proactive security measures can effectively reduce vulnerabilities and enhance cloud security resilience. 
