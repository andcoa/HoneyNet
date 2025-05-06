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

Created a Windows VM which will act as a honeypot.

![image](https://github.com/user-attachments/assets/97f0bd63-0e99-4b0b-9040-ad055cc83d64)

Opening up the VM's firewall by adding an inbound security rule allowing all inbound connections, not just RDP.

![image](https://github.com/user-attachments/assets/c847551c-9100-441a-b6b5-4c316775fd45)

![image](https://github.com/user-attachments/assets/899a2fa9-b212-4144-99de-595615731623)

Logged in the Windows 10 VM by pasting in the public IP address provided by Azure.

![image](https://github.com/user-attachments/assets/05da2164-28d3-4239-9298-4c83198fe763)

![image](https://github.com/user-attachments/assets/1ffb48f0-e85c-484f-aba9-aab0094d5b26)

Disabled the internal firewall on the Windows 10 VM.

![image](https://github.com/user-attachments/assets/aad78b7c-8045-431a-be0c-016424382978)

![image](https://github.com/user-attachments/assets/300ebce5-ffa4-4316-bde7-4c28f3cc61f4)

![image](https://github.com/user-attachments/assets/d2cedd94-7bb2-4464-9c3f-e41bdc855d5c)

![image](https://github.com/user-attachments/assets/3656a86a-c902-4204-bffb-a14c84d648f2)

![image](https://github.com/user-attachments/assets/04e96c56-9b20-4080-8810-45f97978e971)

Successfully pinged the Windows 10 VM from a real machine.

![image](https://github.com/user-attachments/assets/19f78e7f-0272-4fcd-9a65-58e2f5ace101)

Tried to log in the Windows 10 VM by entering wrong credentials to generate logs.

![image](https://github.com/user-attachments/assets/e0199e13-1a44-4fc9-907f-13c6b9d95f2e)

![image](https://github.com/user-attachments/assets/e3e9b448-1e05-4c41-be51-05bd72511221)

In Event Viewer on the Windows 10 VM, filtered for Event ID 4625 (failed logon attempt)

![image](https://github.com/user-attachments/assets/ce8b2c37-b271-4cba-b319-78c2cd72b4cf)

Started seeing failed login attempts from unknown attackers within 10 minutes of changing the VM's firewall rules.

![image](https://github.com/user-attachments/assets/e3063857-91d2-45ad-a877-d7f1fd506664)

Configured an Azure log repository to forward the Windows 10 VM's logs. The Log Analytics workspace was assigned to the Resource Group created earlier on the East US 2 region (same as the target VM).

![image](https://github.com/user-attachments/assets/1925e2fd-b895-401c-be4b-65c7747e1bdc)

![image](https://github.com/user-attachments/assets/e2058776-1ebe-4e96-bd5b-9b8d7a430f5f)

Created a Microsoft Sentinel instance by adding the Log Analytics Workspace to it. Sentinel will be used as a SIEM to see the logs collected from the Windows 10 VM.

![image](https://github.com/user-attachments/assets/bb688e11-40d5-4a35-9556-5d0b271f5fbc)


