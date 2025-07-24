# AzureArc-DNS-Deployment
# 🛰️ Hybrid DNS Deployment on Non-Azure Machine using Azure Arc & Custom Script Extension

## 📘 Project Summary

This project demonstrates how to automate the installation of the DNS Server role on a non-Azure Windows Server by leveraging **Azure Arc**, **Azure Storage Account**, and the **Custom Script Extension**.

The target server was Arc-enabled and managed from the Azure Portal. A PowerShell script was hosted in Azure Storage and executed remotely using Azure Arc extension services to configure DNS.

---

## 🚀 Technologies Used

- Azure Arc for Servers
- Windows Server 2022
- PowerShell
- Azure Storage Account (Blob)
- Azure CLI
- Azure Custom Script Extension
- Role-Based Access Control (RBAC)

---
## 🧪 How It Works

1. Azure Arc agent installed on the on-premises server.
2. Server registered and visible in Azure Arc (Connected Machine).
3. PowerShell script uploaded to Azure Storage Blob.
4. Custom Script Extension triggered via Azure CLI.
5. Script pulled from storage and executed on the server.
6. DNS Server role installed, and DNS zone + sample record configured.

---

## 🔐 Security Considerations

- Used public blob access only for demo purposes.
- In production, consider using SAS tokens or private endpoints.
- Applied Azure RBAC to limit extension deployment rights.

---

## ✅ Sample PowerShell Script

```powershell
Install-WindowsFeature -Name DNS -IncludeManagementTools
Add-DnsServerPrimaryZone -Name "midotop.com" -ZoneFile "midotop.com.dns"
Add-DnsServerResourceRecordA -Name "www" -ZoneName "midotop.com" -IPv4Address "192.168.1.100"

---
## 🧩 Project Architecture

```mermaid
flowchart TD
    LocalMachine[On-Prem Windows Server]
    AzureArc[Azure Arc Agent]
    Azure[Azure Portal]
    Blob[Azure Storage Account<br>Blob Container]
    Script[Install-DNS.ps1]
    Extension[Custom Script Extension]

    LocalMachine --> AzureArc --> Azure
    Azure --> Extension
    Extension --> Blob
    Blob --> Script --> LocalMachine

    LocalMachine --> AzureArc --> Azure
    Azure --> Extension
    Extension --> Blob
    Blob --> Script --> LocalMachine
