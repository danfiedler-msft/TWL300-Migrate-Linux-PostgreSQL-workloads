---
title: Introduction
layout: home
nav_order: 1
---

# TechWorkshop L300 - Migrate and modernize workloads to Azure - Linux and PostgreSQL

## Overview

In this lab, you'll plan and execute a migration of a representative Linux workload from an on-premises datacenter to **Microsoft Azure**. You'll use **Azure Migrate** to discover and assess the environment, choose modernization paths, and then migrate both a database tier (PaaS) and an application tier (IaaS). Finally, you'll apply post-migration operational controls for security, backup, monitoring, and cost governance.


## Case study: Linux Migrate
**Terra Firm Laboratories** is a global bioengineering company and a leading researcher in genetic and biological science technology. Founded in 1975, Terra Firm's headquarters are in Palo Alto, CA. Mission-critical workloads are currently hosted in an on-premises datacenter, and the organization is beginning a journey to modernize and migrate into the cloud using Microsoft Azure.

The CTO, **Dennis Nedry**, has initiated an effort to adopt Azure and modernize infrastructure by reducing technical debt and streamlining operations using **Infrastructure as a Service (IaaS)** and **Platform as a Service (PaaS)** capabilities. Terra Firm completed an initial analysis across more than 250 workloads and selected one workload to validate the migration plan end-to-end. The environment includes multiple Linux distributions (RHEL, SUSE, Ubuntu, and a Debian-based custom distro). The company currently uses **FreeIPA** for identity management and wants to migrate to **Microsoft Entra ID**.

## Architecture

In this lab, you work with:
- An on-premises-style **Hyper-V host** running Linux virtual machines.
- An **Azure Migrate project + appliance** used to discover servers and workloads and generate assessments.
- A **PaaS target** for PostgreSQL using **Azure Database for PostgreSQL Flexible Server** (private access).
- An **IaaS target** using **Azure VM migration** (Azure Migrate Server Migration).
- Post-migration operations controls (backup, patching, security posture, monitoring, and cost management).

## Exercises

This lab includes the following exercises:

- **Exercise 00**: Prepare for workload migration with Azure Migrate and discover workloads on Hyper-V host (**25 minutes**)
- **Exercise 01**: Assess on-prem workload readiness for migration (**45 minutes**)
- **Exercise 02**: Migrate PostgreSQL to Azure Database for PostgreSQL Flexible Server (**50 minutes**)
- **Exercise 03**: Migrate Linux middleware/runtime server using Azure Migrate (**75 minutes**)
- **Exercise 04**: Governance, security, and cost optimization (**30 minutes**)
- **Exercise 05**: Modernize a legacy app for AKS Automatic with GitHub Copilot


## Prerequisites


- Basic familiarity with the **Azure portal** (resource groups, search, blades).
- Comfort using a browser-based lab environment and switching between tabs/windows.
- Basic Linux navigation concepts (you'll use provided commands and credentials).
- Basic understanding of migration concepts:
  - Discovery and assessment
  - Cutover and validation
  - Rollback and operational readiness

## Lab set-up prerequisites
The exercises in this repository were designed for a pre-configured hosted lab environment. If you're following along in your own environment, you'll want to make sure you've setup and configured these resources before getting started.

#### On-prem / lab environment
These exercises assume a fully functional Hyper-V virtualization setup with a multi-tier application already deployed and running.
 
- A Windows jump box with connectivity to both your on-prem resources and Azure
- The Azure Migrate appliance deployed on the jump box using the PowerShell deployment option
- The Azure Migrate Appliance Configuration Manager installed and accessible from the jump box desktop
- A Hyper-V host (the lab references this as `hyperv-01`) with RDP access configured from the jump box
- Working Hyper-V admin credentials
- The Azure Site Recovery Provider (`AzureSiteRecoveryProvider.exe`) must be installable on the host
- Two Linux guest VMs running on the Hyper-V host: one serving as the application frontend and one as the backend
- A working Airsonic application already installed and reachable over HTTP on port 8080 (e.g., `http://airsonic-frontend:8080/airsonic`)
- A working PostgreSQL server already installed and reachable on port 5432
- An existing PostgreSQL database named `airsonic`
- The Airsonic configuration file (`/var/airsonic/airsonic.properties`) already pointed at the source PostgreSQL database
- Working credentials for the Linux VMs, PostgreSQL, and the Airsonic application
- DNS/name resolution working across the environment (the lab expects hostnames like `hyperv-01`, `airsonic-frontend`, and `airsonic-backend` to resolve correctly)
- PuTTY (or an equivalent SSH client) installed on the jump box
- A VPN client connectivity script or equivalent mechanism in place
- The environment must be discoverable by Azure Migrate, including server names and workload identifiers (e.g., the lab expects to discover `Airsonic-Frontend`, `Airsonic-Backend`, a web app named `airsonic`, and a database workload named `airsonic-backend`)
 
## Azure environment
 
The following Azure resources and access must be provisioned before starting the exercises.
 
- An active Azure subscription with learner credentials
- A resource group for migration resources (the lab uses `AZMigrateRG`)
- A virtual network with a subnet suitable for flexible server deployment
- A storage account for replication data
- Hybrid connectivity (such as a VPN) between your on-prem environment and Azure
- RBAC permissions and Azure Policy settings that allow creation and management of Azure Migrate replication and migration resources

{: .note }
> **Tip:** If any of these areas are new to you, we recommend reviewing the relevant Microsoft Learn modules before diving into the exercises. The hosted lab version of this content handles all of this setup for you automatically.
