# Azure Security Lab: SOC, Honeynet, and Log Analytics
![image](https://github.com/isaac-daniel00/Cloud-SOC/assets/155948481/66974b07-6480-4c23-a6c6-a46d32584486)

## Introduction

In the course of this project, I've constructed a compact honeynet within the Azure environment. The architecture for the honeynet consists of:

- Virtual Network
- Network Security Group
- Virtual Machines
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

Log sources from diverse resources have been funneled into a Log Analytics workspace. Microsoft Sentinel, leveraging this workspace, is employed to craft attack maps, initiate alerts, and manage incidents. The project involves a structured process using Microsoft Sentinel: initially measuring security metrics in the less secure environment over 24 hours, implementing security controls to fortify the setup, measuring metrics for an additional 24 hours, and presenting the outcomes. The metrics used in Microsoft Sentinel encompass:

- SecurityEvent
- Syslog
- SecurityAlert
- SecurityIncident
- AzureNetworkAnalytics_CL

At the project's outset, the initial metrics, or "before" metrics, showed that all resources were openly exposed to the internet. Virtual Machines had loose security setups, allowing unrestricted access. Additionally, various resources had public endpoints, making Private Endpoints unnecessary. Later on, significant security improvements were made. The "after" metrics, assessed after the initial 24 hours, depicted a much stronger setup. Network Security Groups were revamped to allow connections only from a designated admin workstation. Built-in firewalls on Virtual Machines were activated, and Private Endpoints were added, enhancing the overall security.

## Azure Sentinel
Azure Sentinel, as a robust Security Information and Event Management (SIEM) tool, played a crucial role. It helped create detailed attack maps from carefully imported logs, giving a clear view of potential threats. The platform also simulated attack traffic through a dedicated virtual machine (VM), allowing for controlled testing of system responses.

Azure Sentinel continued to be key in maintaining a proactive security stance. This involved setting up custom alerts to quickly spot and respond to malicious activities, contributing to structured incident management. In line with improving the overall security, the project followed the rigorous guidelines of NIST 800-61 and NIST 800-53 standards. This ensured a thorough approach to incident response and system hardening. A careful analysis was conducted to measure the impact of these security measures, offering valuable insights into their effectiveness in strengthening the Azure environment.

## NIST 800-61

In alignment with NIST 800-61 guidelines, a systematic approach to incident handling was followed. The preparedness phase involved the logging of relevant logs into the Log Analytics workspace, establishing a foundation for effective incident detection and analysis. During the detection and analysis phase, incident severity, status, and ownership were diligently managed to ensure a swift and targeted response.

Subsequent stages, encompassing containment, eradication, and recovery, were executed with the implementation of a customized response playbook. This proactive approach facilitated the containment of incidents, eradication of threats, and the subsequent recovery of affected systems. Finally, in the post-incident activity phase, meticulous documentation of findings took place, and incidents were systematically closed within Microsoft Sentinel. This comprehensive adherence to NIST 800-61 guidelines not only ensures a structured response to security incidents but also contributes to continuous improvement in incident management practices within the Azure environment.

## NIST 800-53

In the pursuit of fortifying the security posture within the Azure environment, comprehensive measures were undertaken to adhere to the standards outlined in the NIST 800-53 framework. Specifically, these measures were applied within the context of Microsoft Defender for Cloud, a robust security solution designed to safeguard cloud environments.

Following the activation of NIST 800-53 compliance measures, a thorough assessment of the secure score in Microsoft Defender for Cloud was conducted. The secure score serves as a quantitative representation of an organization's security posture, offering insights into the effectiveness of implemented security controls and highlighting areas that may require further attention and enhancement. This initiative not only exemplifies a commitment to aligning with industry-recognized security standards but also underscores a proactive approach to cybersecurity within the dynamic landscape of cloud environments. By leveraging Microsoft Defender for Cloud in tandem with NIST 800-53 compliance measures, the organization establishes a resilient security foundation, instilling confidence in the robustness of its security controls and readiness to mitigate emerging threats.

## Attack maps before implementing and hardening Security controls
![nsg-mal](https://github.com/isaac-daniel00/Cloud-SOC/assets/155948481/7b2877ae-2ce6-4125-b04f-6f67e25b51b5)
![Linux-ssh](https://github.com/isaac-daniel00/Cloud-SOC/assets/155948481/9e0ae808-a78a-4b9c-a2c1-27b95350f25a)
![windows-rdp](https://github.com/isaac-daniel00/Cloud-SOC/assets/155948481/fa5ed3be-3ba6-402d-a0ac-7fabd5dc4848)

## Metrics before implementing and hardening Security controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
- Start Time 2024-01-06 23:37:52
- Stop Time 2024-01-07 23:37:52

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 34404
| Syslog                   | 7413
| SecurityAlert            | 0
| SecurityIncident         | 260
| AzureNetworkAnalytics_CL | 3977

## Attack maps after implementing and hardening Security controls

```There were no instances of malicious activity during the 24 hour period. ```

## Metrics after implementing and hardening Security controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
- Start Time: 2024-01-07 01:02:39
- Stop Time: 2024-01-0801:02:39

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 1
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this Azure-based project, we established a compact honeynet with integrated log sources managed through a Log Analytics workspace. Microsoft Sentinel generated alerts and incidents from the aggregated logs. Our evaluation encompassed measuring metrics in the insecure environment prior to the implementation of security controls and subsequently after their application. Significantly, the post-implementation phase exhibited a remarkable reduction in both security events and incidents, underscoring the efficacy of the implemented security measures.

It is essential to acknowledge that if the network resources had been heavily utilized by regular users, the 24-hour period following the enforcement of security controls might have yielded a higher volume of security events and alerts. This consideration underscores the dynamic nature of security assessments and the potential impact of real-world network usage on observed metrics.
