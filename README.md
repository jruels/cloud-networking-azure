# Azure Cloud Networking

This repository contains hands-on labs for the Azure Cloud Networking course. Complete the labs in Azure Cloud Shell or the Azure Portal.

## Repository Structure

- Labs/  
 # Hands-on labs for Day 1:
  - [Lab1.md](Day1/Lab1/Lab1.md) – Provision an Azure Virtual Network  
  - [Lab2.md](Day1/Lab2/Lab2.md) – Creating Subnets in an Existing Azure Virtual Network
  - [Lab3.md](Day1/Lab3/Lab3.md) – Implement User-Defined Routes  
  - [Lab4.md](Day1/Lab4/Lab4.md) – Deploy a NAT Gateway  
  - [Lab5.md](Day1/Lab5/Lab5.md) – Configure RBAC for Network Resources  
  - [Lab6.md](Day1/Lab6/Lab6.md) – Deploying Azure Firewall  

  # Hands-on labs for Day 2:
  - [Lab7.md](Day2/Lab7/Lab7.md) – Creating a Public DNS Zone and Records in Azure DNS  
  - [Lab8.md](Day2/Lab8/Lab8.md) – Setting Up a Private DNS Zone in Azure  
  - [Lab9.md](Day2/Lab9/Lab9.md) – Configuring Azure Traffic Manager for Performance Routing  
  - [Lab10.md](Day2/Lab10/Lab10.md) – Implementing Azure CDN for Content Caching  
  - [Lab11.md](Day2/Lab11/Lab11.md) – Deploying VMs with Availability Zones for Resilience  
  - [Lab12.md](Day2/Lab12/Lab12.md) – Automating Network Deployment with Terraform  

## Prerequisites

- An active Azure subscription  
- Owner or Network Contributor role on target resource group  
- Azure CLI installed (for shell labs) or access to the Azure Portal  

## How to Use

1. Clone or download the repository.  
2. To run a lab:
   - Open Azure Cloud Shell (Bash) or a local terminal with `az` authenticated.
   - Navigate to the lab folder, e.g.:
     ```bash
     cd Labs/Day1/Lab1
     code Lab1.md  # or open in your editor
     ```
   - Follow the steps in the lab markdown file.
---
