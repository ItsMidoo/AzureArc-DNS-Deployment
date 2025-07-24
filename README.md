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
