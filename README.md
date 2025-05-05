# Azure HoneyNet

## Objective

Deploy a publicly exposed Windows VM in Azure to act as a honeynet, collect attacker telemetry using Azure Monitor and Log Analytics, and visualize global threat data through Microsoft Sentinel.

## Skills Learned

- Cloud Network Configuration: Built a virtual network, subnet, and fully open security group to simulate an internet-facing target.
- Honeypot Design on Azure: Intentionally exposed a VM to the public to attract brute-force attacks and log malicious activity.
- Log Collection & Forwarding: Installed and configured the Azure Monitoring Agent to forward Windows security events to Log Analytics.
- Sentinel SIEM Dashboards: Connected Sentinel to the Log Analytics workspace and built custom dashboards for visualizing failed logins and attacker geolocation.
- Watchlist-Driven Analysis: Used IP block watchlists in Sentinel queries to enrich attacker telemetry with geographic context.

## Tools Used

- Microsoft Azure: For provisioning and managing cloud infrastructure.
- Windows VM: Target system exposed to the internet to attract attacks.
- Log Analytics Workspace: Centralized repository for log data.
- Azure Monitor Agent: Forwarder for Windows event logs.
- Microsoft Sentinel: SIEM platform used for querying logs and building dashboards.
- Watchlists (CSV): Used in Sentinel KQL queries to correlate IPs with geolocation.

## Steps

Lab diagram:

![image](https://github.com/user-attachments/assets/742a4f9c-62fd-411c-a846-20b68b97d48d)

Signed up for Microsoft Azure.

![image](https://github.com/user-attachments/assets/41a40919-e52e-49ef-aaf2-6543d600e2c3)

Created the Resource Group.

![image](https://github.com/user-attachments/assets/2aab083a-a6bc-40c2-8cb7-0f33e28e70f3)

Deployed the Virtual Network in the Resource Group created above.

![image](https://github.com/user-attachments/assets/82113ce4-6ab2-4059-b0b5-70b155f821fd)

Created a Windows VM Honeypot.

![image](https://github.com/user-attachments/assets/60b914f4-5de3-4e95-a562-55ea59c35d9b)



