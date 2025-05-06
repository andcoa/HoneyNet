# Microsoft Azure SOC HoneyNet

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

![image](https://github.com/user-attachments/assets/1cac2688-61d9-4137-9182-b0c565c166ed)

![image](https://github.com/user-attachments/assets/bb34ad9f-6987-4a4c-bafd-35123c26af87)

Installed Windows Security Events in Sentinel.

![image](https://github.com/user-attachments/assets/fce5eac5-c633-4bc7-a098-22c062fc6ebd)

![image](https://github.com/user-attachments/assets/5fec188e-1438-4b05-8ea6-cc6d993690e2)

Configured Windows Security Events to create a connection between the Log Analytics Workspace and the Windows 10 VM.

![image](https://github.com/user-attachments/assets/1f136c6e-43ea-4175-83a1-54e9295a6a6e)

Created a data collection rule to forward logs from the Windows 10 VM to the Log Analytics Workspace.

![image](https://github.com/user-attachments/assets/b40bb919-cc58-4d6d-8fca-544c35245194)

![image](https://github.com/user-attachments/assets/cdce691d-69d2-45e8-90c2-62ea34835e7e)

![image](https://github.com/user-attachments/assets/0da40771-59a5-4e08-851f-3b51b3dfb111)

![image](https://github.com/user-attachments/assets/0f02c423-7882-46d5-a0e4-647cfacbfb9d)

The connector was successfully added to the VM.

![image](https://github.com/user-attachments/assets/528832e1-a405-485c-8a14-d2b36d4aed4c)

Accessed the collected logs by going in the Log Analytics Workspace and query for "SecurityEvent".

![image](https://github.com/user-attachments/assets/9af0f780-6857-49fa-927f-906090fa1bf5)

Used KQL to create query that sorts logs by the account "ADMINISTRATOR" and only shows the fields TimeGenerated, Account, Computer, EventID, Activity and IpAddress. There are 24 instances of failed logon attempts by attackers on the public internet using the credential "ADMINISTRATOR".

![image](https://github.com/user-attachments/assets/31b00a42-f7cb-404f-b2a5-47e476bc5d97)

Wrote another KQL query to see the logs collected within the last 5 minutes containing the EventID 4625 (failed logon attempt).

![image](https://github.com/user-attachments/assets/99740969-ff04-489f-bdec-26e3c2a6d0c6)

Used the following list to create a geolocation watchlist in Sentinel:

![image](https://github.com/user-attachments/assets/bfaf48f3-456f-4cc0-9fd2-b3a26c29169c)

In Sentinel, created a new Watchlist:

![image](https://github.com/user-attachments/assets/2df226a3-3a15-4da3-a0a5-b41fcbf28593)

![image](https://github.com/user-attachments/assets/344a5505-4085-46e4-a46f-22cf317106ca)

Uploaded the geolocation file.

![image](https://github.com/user-attachments/assets/3cc068d7-de00-48ee-b447-9ebf9f84e6a5)

Successfully created the geoip Watchlist.

![image](https://github.com/user-attachments/assets/41a2de54-1f86-41f0-97cf-a1a305677f86)

![image](https://github.com/user-attachments/assets/6b7eb527-f8a1-4bfd-8a9b-a80aac28cfe1)

The Watchlist can now be queried for with KQL in the Log Analytics Workspace.

![image](https://github.com/user-attachments/assets/9349d991-453c-4f0a-8857-fd4cd311fed3)

Wrote a query to display the location of one of the attackers. The query filters for the IP of the attacker and the EventID 4625 (failed logon attempt), displaying all data under the fields of my chosing.

![image](https://github.com/user-attachments/assets/4add7836-6ac2-4d54-8a74-fa08a6199843)

Created the Attack Map in a Sentiel Workbook.

![image](https://github.com/user-attachments/assets/60c0e9dc-37e2-4941-8892-a4408bec078e)

![image](https://github.com/user-attachments/assets/cf6a8bc0-e146-4280-93bb-81619cf2b63d)

Used the following JSON script to set up the Workbook.

![image](https://github.com/user-attachments/assets/1932e14d-2bec-4443-99dc-9cb2b3637ebd)

![image](https://github.com/user-attachments/assets/30bc05f8-cec7-4c0f-8fc1-2cc649933e4c)

Saved the Attack Map under the Resource Group created earlier.

![image](https://github.com/user-attachments/assets/317e6770-0f61-4d1e-8321-580dbc92bfd3)

The following Attack Map was created:

![image](https://github.com/user-attachments/assets/51072a90-f0c2-4998-ba31-4b22440a2a70)

The map is also highly customizable:

![image](https://github.com/user-attachments/assets/907e129c-857e-4836-9c31-904c1e5d47a8)

![image](https://github.com/user-attachments/assets/763e0634-623c-4b15-9826-8bee80e2c34f)




