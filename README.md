# Enterprise Hybrid Infrastructure

## Overview

This project is an enterprise-style hybrid infrastructure built using VMware Workstation and Microsoft Azure. It combines an on-premises virtual network with a cloud environment connected through a site-to-site VPN, simulating a real-world enterprise network.

The infrastructure includes Active Directory, DNS, DHCP, VLAN segmentation, OPNsense firewall, Windows and Linux servers, Azure Hub-and-Spoke networking, Azure Firewall, Azure Bastion, and centralized monitoring.

The project demonstrates enterprise networking, cloud integration, virtualization, infrastructure administration, and network security.

---

# Architecture

The environment consists of the following technologies:

### On-Premises Infrastructure

* VMware Workstation
* OPNsense Firewall
* Windows Server 2025
* Active Directory Domain Services (AD DS)
* DNS
* DHCP
* Windows 11 Client
* Ubuntu Server
* Ubuntu Desktop
* VLAN Segmentation

### Azure Cloud Infrastructure

* Azure Virtual Network (Hub-and-Spoke)
* Azure Firewall
* Azure Bastion
* Virtual Machines
* Network Security Groups (NSGs)
* Site-to-Site VPN
* Azure Monitor
* Log Analytics Workspace

---

# Project Objectives

* Build an enterprise-grade hybrid network.
* Simulate an on-premises corporate environment.
* Integrate Azure cloud networking with local infrastructure.
* Implement secure network segmentation.
* Provide centralized authentication using Active Directory.
* Secure communication using VPN connectivity.
* Demonstrate enterprise firewall configuration.
* Implement cloud monitoring and security.

---

# Network Topology

The infrastructure contains:

### On-Premises

* OPNsense Firewall
* LAN Network
* DMZ Network
* Domain Controller
* Windows Client
* Ubuntu Server
* Ubuntu Desktop

### Azure

* Hub Virtual Network
* Shared Services Subnet
* Azure Firewall
* Azure Bastion
* Gateway Subnet
* VPN Gateway

The on-premises environment communicates securely with Azure through a Site-to-Site VPN.

---

# Architecture Diagram

*Insert Architecture Diagram Here*

---

# Technologies Used

### Virtualization

* VMware Workstation

### Networking

* OPNsense
* VLANs
* Routing
* DHCP
* DNS
* VPN
* NAT
* Firewall Rules

### Windows

* Windows Server 2025
* Active Directory
* Group Policy
* DNS
* DHCP

### Linux

* Ubuntu Server
* Ubuntu Desktop

### Cloud

* Microsoft Azure
* Azure Virtual Networks
* Azure Firewall
* Azure Bastion
* Network Security Groups
* VPN Gateway
* Azure Monitor
* Log Analytics

---

# Implementation

## 1. VMware Environment

Built the virtual infrastructure using VMware Workstation.

Created isolated virtual networks for:

* WAN
* LAN
* DMZ

---

## 2. OPNsense Firewall

Configured OPNsense as the enterprise firewall.

Responsibilities include:

* Routing
* NAT
* Firewall Rules
* DHCP
* Network Segmentation
* VPN Connectivity

---

## 3. Active Directory

Installed Windows Server 2025.

Configured:

* Active Directory Domain Services
* Organizational Units
* Users
* Groups
* DNS
* DHCP

---

## 4. Client Systems

Joined Windows 11 workstations to the Active Directory domain.

Configured:

* Domain authentication
* DNS resolution
* DHCP
* Network connectivity

---

## 5. Linux Servers

Deployed Ubuntu Server and Ubuntu Desktop virtual machines.

Configured:

* Static IP addressing
* SSH
* Network connectivity
* Firewall configuration

---

## 6. Azure Networking

Built an enterprise Hub-and-Spoke architecture including:

* Hub Virtual Network
* Shared Services Subnet
* Azure Firewall
* Azure Bastion
* Gateway Subnet

Configured peering and routing between Azure resources.

---

## 7. Hybrid Connectivity

Configured a Site-to-Site VPN connecting VMware and Azure.

Validated:

* Connectivity
* Routing
* Secure communication
* Resource accessibility

---

## 8. Security

Implemented:

* Firewall policies
* Network segmentation
* NSGs
* VPN encryption
* Secure remote administration using Azure Bastion

---

## 9. Monitoring

Configured monitoring using:

* Azure Monitor
* Log Analytics

Collected:

* Connectivity information
* VM health
* Security events
* Diagnostic logs

---

# Screenshots

### Network Diagram

*Architecture Diagram*

---

### VMware Environment

*VM Inventory*

---

### OPNsense Dashboard

*Firewall Dashboard*

---

### Interface Configuration

*WAN / LAN / DMZ Interfaces*

---

### Firewall Rules

*Firewall Rules Screenshot*

---

### Windows Server

*Server Manager*

---

### Active Directory

*Users and Computers*

---

### DNS

*DNS Manager*

---

### DHCP

*DHCP Console*

---

### Windows Client

*Domain Joined Workstation*

---

### Ubuntu Server

*SSH Session*

---

### Azure Resource Group

*Azure Resource Group*

---

### Hub Virtual Network

*Hub VNet*

---

### Azure Firewall

*Firewall Configuration*

---

### Azure Bastion

*Bastion Configuration*

---

### VPN Gateway

*VPN Gateway*

---

### Successful VPN Connection

*Tunnel Status*

---

### Azure Monitor

*Monitoring Dashboard*

---

# Challenges and Troubleshooting

During development, several issues were encountered and resolved.

## Virtual Networking

Configured VMware virtual networks to properly separate WAN, LAN, and DMZ traffic while maintaining connectivity.

## Firewall Configuration

Developed and tested firewall rules to allow only required communication between network segments.

## Active Directory Integration

Verified DNS, DHCP, and domain services before joining client systems.

## VPN Connectivity

Resolved routing and gateway configuration issues to establish secure communication between the on-premises network and Azure.

## Azure Networking

Validated virtual network peering, subnet configuration, and Azure Firewall routing.

These troubleshooting activities strengthened practical knowledge of enterprise networking, hybrid cloud architecture, and infrastructure administration.

---

# Skills Demonstrated

* Enterprise Networking
* Hybrid Cloud Infrastructure
* VMware Virtualization
* Microsoft Azure
* Active Directory
* Windows Server Administration
* OPNsense Firewall
* VLAN Configuration
* Routing and Switching Concepts
* DNS
* DHCP
* VPN Configuration
* Azure Hub-and-Spoke Networking
* Azure Firewall
* Azure Bastion
* Network Security Groups
* Network Troubleshooting
* Infrastructure Administration
* Cloud Networking
* Hybrid Connectivity
* Log Analytics
* Azure Monitor

---

# Future Improvements

Potential enhancements include:

* Multi-site branch office connectivity
* High Availability firewalls
* Active Directory replication
* Azure Load Balancer
* Web server hosted in the DMZ
* Web Application Firewall
* Microsoft Sentinel integration
* Infrastructure as Code using Terraform or Bicep
* Automated VM deployment
* Centralized logging using SIEM

---

# Project Outcome

The completed hybrid infrastructure successfully integrates an enterprise on-premises environment with Microsoft Azure. The solution provides centralized identity management, secure network segmentation, hybrid VPN connectivity, cloud networking, monitoring, and enterprise-grade firewall protection.

This project demonstrates practical experience with enterprise networking, Windows Server administration, virtualization, cloud infrastructure, and hybrid cloud architecture using technologies commonly found in production enterprise environments.
