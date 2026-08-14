# Enterprise Hybrid Infrastructure

## Overview

This project is an enterprise-style hybrid infrastructure environment built using VMware Workstation, OPNsense, Windows Server, Linux, and Microsoft Azure.

The project simulates an on-premises corporate network containing separate LAN and DMZ segments, centralized Windows services, client and server systems, and an OPNsense firewall. The on-premises environment is connected to an Azure virtual network through a functional **IKEv2/IPsec Site-to-Site VPN between OPNsense and an Azure VPN Gateway**.

Private communication between the VMware environment and an Azure virtual machine was successfully established and validated across the VPN tunnel.

The project demonstrates practical experience with enterprise networking, virtualization, firewall administration, Windows infrastructure, Linux, Azure networking, IPsec VPN configuration, routing, and hybrid-cloud troubleshooting.

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
* LAN and DMZ Network Segmentation

### Azure Cloud Infrastructure

* Microsoft Azure
* Hub Virtual Network
* Dedicated Azure Subnets
* Network Security Groups (NSGs)
* Azure VPN Gateway
* Local Network Gateway
* Site-to-Site IKEv2/IPsec VPN
* Azure Windows Server Virtual Machine

---

# Project Objectives

* Build an enterprise-style virtual network.
* Simulate an on-premises corporate infrastructure.
* Separate internal and DMZ workloads into different network segments.
* Configure OPNsense for routing, firewalling, and VPN connectivity.
* Implement centralized authentication and DNS using Active Directory.
* Build an Azure network designed around a hub architecture.
* Establish secure Site-to-Site connectivity between VMware and Azure.
* Validate private communication between on-premises and cloud resources.
* Gain hands-on experience troubleshooting hybrid networking and IPsec.

---

# Network Topology

The infrastructure contains:

### On-Premises

* OPNsense Firewall
* LAN — `192.168.10.0/24`
* DMZ — `192.168.20.0/24`
* Windows Server Domain Controller
* Windows 11 Client
* Ubuntu Server
* Ubuntu Desktop

### Azure

* Hub Virtual Network — `10.0.0.0/16`
* Gateway Subnet
* Shared Services Subnet
* Reserved subnets for future Azure services
* Azure VPN Gateway
* Azure Windows Server VM — `10.0.1.4`

The two environments communicate through an **IKEv2/IPsec Site-to-Site VPN**.

The VPN establishes private connectivity between:

`192.168.10.0/24 ↔ 10.0.0.0/16`

---

# Architecture Diagram

*Insert Architecture Diagram Here*

---

# Technologies Used

### Virtualization

* VMware Workstation

### Networking

* OPNsense
* IPv4 Subnetting
* Routing
* NAT
* Firewall Rules
* LAN/DMZ Segmentation
* IKEv2
* IPsec
* Site-to-Site VPN

### Windows

* Windows Server 2025
* Active Directory Domain Services
* DNS
* DHCP
* Windows 11

### Linux

* Ubuntu Server
* Ubuntu Desktop
* Linux Network Configuration
* SSH

### Cloud

* Microsoft Azure
* Azure Virtual Networks
* Azure Subnets
* Network Security Groups
* Azure VPN Gateway
* Local Network Gateway
* Azure Virtual Machines

---

# Implementation

## 1. VMware Environment

Built the on-premises virtual infrastructure using VMware Workstation.

Created separate VMware networks to simulate different enterprise network segments:

* WAN
* LAN
* DMZ

Virtual machines were assigned to their appropriate network segments to simulate internal and isolated server environments.

---

## 2. OPNsense Firewall

Deployed OPNsense as the primary firewall and router between the virtual network segments and external networks.

Configured OPNsense for:

* WAN connectivity
* LAN routing
* DMZ routing
* NAT
* Firewall rules
* Network segmentation
* IKEv2/IPsec VPN connectivity

OPNsense also served as the on-premises VPN endpoint for the Azure Site-to-Site connection.

---

## 3. Active Directory

Deployed Windows Server 2025 to provide centralized Windows infrastructure services.

Configured:

* Active Directory Domain Services
* Organizational Units
* Users
* Groups
* DNS
* DHCP

The environment uses an internal Active Directory domain for centralized identity and system administration.

---

## 4. Client Systems

Deployed Windows 11 clients within the LAN environment.

Configured and tested:

* Domain authentication
* Internal DNS resolution
* DHCP
* LAN connectivity
* Gateway connectivity

This provided a client environment for validating the Windows domain and network infrastructure.

---

## 5. Linux Systems

Deployed Ubuntu Server and Ubuntu Desktop virtual machines within the VMware environment.

Configured:

* IP addressing
* Default gateways
* SSH
* Basic Linux networking
* Connectivity testing

Linux systems were included to provide a mixed Windows/Linux enterprise environment and test communication across network segments.

---

## 6. Azure Networking

Created an Azure hub network using the address space:

`10.0.0.0/16`

The hub was divided into dedicated subnets for infrastructure services, including:

* `GatewaySubnet`
* Shared Services subnet
* Reserved Azure Firewall subnet
* Reserved Azure Bastion subnet

The Firewall and Bastion subnets were included in the network design for future expansion; the core implementation focused on the **VPN Gateway and hybrid connectivity**.

An Azure Windows Server VM was deployed into the Shared Services subnet with the private IP:

`10.0.1.4`

Network Security Group rules were configured as needed to permit testing between the on-premises and Azure environments.

---

## 7. Azure Site-to-Site VPN

Configured a Site-to-Site VPN directly between:

**OPNsense ↔ Azure VPN Gateway**

This implementation used **OPNsense's native IPsec implementation rather than StrongSwan**.

The Azure side included:

* Azure VPN Gateway
* Local Network Gateway
* Site-to-Site Connection
* Pre-Shared Key authentication

The OPNsense side included:

* IKEv2 configuration
* Phase 1 / IKE Security Association
* Phase 2 / Child Security Association
* Local and remote traffic selectors
* IPsec firewall rules

The configured private networks were:

**On-Premises:**

`192.168.10.0/24`

**Azure:**

`10.0.0.0/16`

---

## 8. Hybrid Connectivity Validation

After establishing the IPsec tunnel, connectivity was validated between resources on both sides of the hybrid network.

Testing included communication from a VMware LAN system to:

`AZ-SRV01 — 10.0.1.4`

Successful ICMP responses demonstrated that traffic could travel:

**VMware LAN → OPNsense → IPsec Tunnel → Azure VPN Gateway → Azure VM**

OPNsense IPsec status was also used to verify that the IKE and Child Security Associations were successfully established.

This provided end-to-end confirmation that the Site-to-Site VPN was carrying traffic between the private networks.

---

## 9. Network Security

Implemented multiple layers of network security, including:

* OPNsense firewall policies
* LAN/DMZ segmentation
* Network Security Groups
* IPsec encryption
* IKEv2 authentication
* Private Azure VM addressing
* Controlled communication between network segments

The Azure VM was accessed and tested using private network connectivity rather than exposing the workload as part of the VPN validation.

---

# Screenshots

### Network Architecture

*Final Hybrid Infrastructure Diagram*

---

### VMware Environment

*VM Inventory*

Demonstrates the virtualized on-premises infrastructure and systems used in the project.

---

### OPNsense Dashboard

*OPNsense Dashboard*

Demonstrates firewall deployment and interface configuration.

---

### OPNsense Interfaces

*WAN / LAN / DMZ Interfaces*

Demonstrates network segmentation between the different VMware networks.

---

### OPNsense Firewall Rules

*Firewall Rules Screenshot*

Demonstrates traffic-control policies between network segments.

---

### Active Directory

*Active Directory Users and Computers*

Demonstrates centralized identity infrastructure.

---

### DNS

*DNS Manager*

Demonstrates internal DNS services for the Active Directory environment.

---

### DHCP

*DHCP Configuration*

Demonstrates automated client network configuration.

---

### Windows Client

*Windows Client Connectivity / Domain Screenshot*

Demonstrates connectivity within the internal LAN.

---

### Linux Systems

*Ubuntu Network Configuration / SSH*

Demonstrates Linux integration into the virtual network.

---

### Azure Resource Group

*Azure Resource Group Screenshot*

Demonstrates the Azure resources deployed for the hybrid environment.

---

### Azure Hub Virtual Network

*Hub VNet and Subnets*

Demonstrates the Azure `10.0.0.0/16` network design and dedicated infrastructure subnets.

---

### Azure VPN Gateway

*Virtual Network Gateway Screenshot*

Demonstrates the Azure endpoint used for Site-to-Site VPN connectivity.

---

### Local Network Gateway

*Local Network Gateway Screenshot*

Demonstrates Azure's representation of the on-premises network and VPN endpoint.

---

### OPNsense IPsec Tunnel

*IPsec Status Screenshot*

Demonstrates established IKE and Child Security Associations between OPNsense and Azure.

---

### Azure VPN Connection

*Connected VPN Screenshot*

Demonstrates successful establishment of the Azure Site-to-Site VPN.

---

### Hybrid Connectivity Test

*Successful Ping to `10.0.1.4`*

Demonstrates actual traffic passing from the VMware LAN through OPNsense and the encrypted IPsec tunnel to the Azure VM.

**This is one of the most important screenshots in the project because it proves the VPN was not merely configured—it successfully carried traffic.**

---

# Challenges and Troubleshooting

One of the primary goals of this project was developing practical troubleshooting experience rather than simply deploying resources.

## VMware Virtual Networking

Configured VMware virtual networks to separate WAN, LAN, and DMZ traffic while maintaining the required routing paths through OPNsense.

---

## OPNsense Routing and Firewalling

Configured and tested firewall rules, NAT behavior, interface addressing, and routing between virtual network segments.

Troubleshooting required determining whether connectivity failures originated from:

* Client configuration
* OPNsense firewall policies
* Routing
* NAT
* VMware virtual networking

---

## IPsec VPN Negotiation

The Site-to-Site VPN required troubleshooting multiple components before connectivity was successfully established.

Troubleshooting included:

* Public vs. private WAN addressing
* NAT behavior
* IKE negotiation
* Authentication configuration
* Pre-Shared Keys
* Phase 1 configuration
* Phase 2 / Child SA configuration
* Local and remote traffic selectors
* IPsec firewall policies

The final tunnel was successfully established between OPNsense and Azure.

---

## End-to-End Connectivity

An established VPN tunnel does not automatically guarantee that workloads can communicate.

Additional troubleshooting included:

* Azure Network Security Groups
* Windows Firewall
* ICMP rules
* Source IP selection
* OPNsense firewall rules
* Private IP addressing
* Routing between the two environments

Successful communication with `10.0.1.4` ultimately confirmed that the complete data path was operational.

---

# Skills Demonstrated

* Enterprise Network Design
* Hybrid Cloud Networking
* VMware Virtualization
* Microsoft Azure
* OPNsense Administration
* Windows Server Administration
* Active Directory
* DNS
* DHCP
* Linux Administration
* LAN/DMZ Segmentation
* IPv4 Addressing and Subnetting
* Routing
* NAT
* Firewall Configuration
* Network Security Groups
* IKEv2
* IPsec
* Site-to-Site VPN Configuration
* Azure VPN Gateway
* Hybrid Connectivity
* Network Troubleshooting
* Cloud Networking
* Infrastructure Administration

---

# Future Improvements

Potential enhancements include:

* Domain joining Azure workloads across the Site-to-Site VPN
* Azure VNet spoke deployment and peering
* Azure Firewall deployment
* Azure Bastion deployment
* Azure Monitor and Log Analytics
* Microsoft Sentinel integration
* DMZ-hosted Nginx web server
* Additional firewall segmentation policies
* Multi-site branch connectivity
* Active Directory replication to Azure
* High-availability firewall architecture
* Infrastructure as Code using Terraform or Bicep
* Automated Azure resource deployment

---

# Project Outcome

The project successfully created a virtualized enterprise-style on-premises network and established secure hybrid connectivity with Microsoft Azure.

A functional **IKEv2/IPsec Site-to-Site VPN was established directly between OPNsense and an Azure VPN Gateway**, connecting the on-premises `192.168.10.0/24` LAN with the Azure `10.0.0.0/16` network.

Private communication between a VMware workload and the Azure Windows Server at `10.0.1.4` was successfully validated across the tunnel.

The project provided hands-on experience configuring and troubleshooting **routing, NAT, firewall policies, IPsec/IKEv2 negotiation, Azure networking, NSGs, Windows/Linux systems, and end-to-end hybrid connectivity**.
