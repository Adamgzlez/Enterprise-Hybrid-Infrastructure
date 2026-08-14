# Enterprise Hybrid Infrastructure

## Overview

This project is an enterprise-style hybrid infrastructure environment built using VMware Workstation, OPNsense, Windows Server, Linux, and Microsoft Azure.

The project simulates an on-premises corporate network containing separate LAN and DMZ segments, centralized Windows services, client and server systems, and an OPNsense firewall. The on-premises environment is connected to an Azure virtual network through a functional IKEv2/IPsec Site-to-Site VPN between OPNsense and an Azure VPN Gateway.

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

<img width="1536" height="1024" alt="Hybrid Lab Topology Picture" src="https://github.com/user-attachments/assets/e4467983-92ef-49ce-ab53-3d25f6b6b4ac" />

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

---

### VMware Environment

<img width="334" height="319" alt="VMware Environment" src="https://github.com/user-attachments/assets/abdef378-1158-4df4-8a2f-ae0c643db447" />

Demonstrates the virtualized on-premises infrastructure and systems used in the project.

---

### OPNsense Interfaces

<img width="1549" height="1753" alt="Interface WAN" src="https://github.com/user-attachments/assets/8ae0d6a4-5f9c-473e-af3b-b015f85e22a7" /> <img width="1483" height="1763" alt="Interface LAN" src="https://github.com/user-attachments/assets/250373a2-8e82-4972-bb40-fdccd7e55d23" /> <img width="1504" height="1765" alt="Interface DMZ" src="https://github.com/user-attachments/assets/3c025bae-39ef-4ffa-aceb-28f064fd6dcf" />


Demonstrates network segmentation between the different VMware networks.

---

### OPNsense Firewall Rules

<img width="2862" height="892" alt="Firewall Rules" src="https://github.com/user-attachments/assets/8ee1c574-5317-4544-91a6-e92c59515878" />

Demonstrates traffic-control policies between network segments.

---

### Active Directory

#### Active Directory Users and Computers

<img width="410" height="150" alt="Finance User" src="https://github.com/user-attachments/assets/fe73607a-ef02-47d1-83db-2534fe7979d8" />
<img width="410" height="150" alt="HR User" src="https://github.com/user-attachments/assets/89972a43-33a7-4170-8431-23ab4fbc4863" />
<img width="410" height="200" alt="IT User" src="https://github.com/user-attachments/assets/8f1cbcd8-b01f-4179-9bb6-1b7e7529bcdc" />
<img width="410" height="250" alt="Workstation User" src="https://github.com/user-attachments/assets/c5a601fb-73e5-4878-bdf2-fa94661d950a" />

Demonstrates centralized identity infrastructure.

---

### DNS

<img width="747" height="128" alt="Domain-Company Name" src="https://github.com/user-attachments/assets/41190b94-fd6e-4ba0-aca7-2b9dd0abadc9" />

Demonstrates internal DNS services for the Active Directory environment.

---

### DHCP

<img width="813" height="453" alt="OPNsense Configuration Edit" src="https://github.com/user-attachments/assets/deba8aad-d5a0-4c21-b316-a7da29084b19" />

Demonstrates automated client network configuration.

---

### Windows Client

*Windows Client Connectivity / Domain Screenshot*

Demonstrates connectivity within the internal LAN.

---

### Linux Systems

#### Ubuntu LAN Connectivity

<img width="884" height="676" alt="Ubuntu Server Connectivity" src="https://github.com/user-attachments/assets/6b4e169f-a255-43d5-aa78-f4bd1b4791df" />

#### Ubuntu DMZ Connectivity

<img width="885" height="547" alt="DMZ Connectivity" src="https://github.com/user-attachments/assets/277b3754-2445-41b3-8cb5-631679383ccb" />

Demonstrates Linux integration into the virtual network.

---

### Azure Resource Group

<img width="1403" height="895" alt="Resource Groups" src="https://github.com/user-attachments/assets/27b59158-ffee-4906-b7ca-c14c39686be7" />

Demonstrates the Azure resources deployed for the hybrid environment.

---

### Azure Hub Virtual Network

<img width="1725" height="437" alt="Azure hub network" src="https://github.com/user-attachments/assets/ca91cc06-bb8b-4673-93fb-db7961d0f2a9" />

Demonstrates the Azure `10.0.0.0/16` network design and dedicated infrastructure subnets.

---

### Azure VPN Gateway

<img width="2035" height="321" alt="Virtual Networks" src="https://github.com/user-attachments/assets/ab5261c8-3e4f-4368-80be-510f574fccfd" />

Demonstrates the Azure endpoint used for Site-to-Site VPN connectivity.

---

### Local Network Gateway

<img width="1977" height="258" alt="Local Network Azure" src="https://github.com/user-attachments/assets/e79eae65-3ca3-483f-85a4-fb8d22bba66f" />

Demonstrates Azure's representation of the on-premises network and VPN endpoint.

---

### OPNsense IPsec Tunnel

<img width="2976" height="745" alt="OPNsense IPsec Status Overview IP Hidden" src="https://github.com/user-attachments/assets/ffbbd176-72a3-4c08-b869-abbdf9983642" />

Demonstrates established IKE and Child Security Associations between OPNsense and Azure.

---

### Azure VPN Connection

<img width="1518" height="219" alt="conn-azure-opnsense connected" src="https://github.com/user-attachments/assets/cfe4331f-c24d-4dba-9ee4-217843cfc01a" />

Demonstrates successful establishment of the Azure Site-to-Site VPN.

---

### Azure VM Overview

<img width="1725" height="637" alt="Azure VM Overview" src="https://github.com/user-attachments/assets/d1009faf-03fc-4093-a7c9-978414c2ff3f" />

Demonstrates that the Azure VM was created from Microsoft Azure

---

### Hybrid Connectivity Test

<img width="832" height="547" alt="Azure VM Connection to OPN - Ping" src="https://github.com/user-attachments/assets/727b7f8e-62d8-4091-96dc-6ec80a454449" />

Demonstrates actual traffic passing from the VMware LAN through OPNsense and the encrypted IPsec tunnel to the Azure VM.

---

### Wireshark Troubleshooting 

<img width="1468" height="861" alt="Wireshark Troubleshoot edited" src="https://github.com/user-attachments/assets/aea473a3-5a91-4b21-a488-cad7d847afed" />

Troubleshooting if packets were coming through IPsec Tunnel.

---

# Challenges and Troubleshooting

One of the primary goals of this project was to develop practical troubleshooting experience rather than simply deploying resources.

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

An established VPN tunnel does not automatically guarantee that workloads can communicate, so I tested connectivity between them using an Azure VM.

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

A functional IKEv2/IPsec Site-to-Site VPN was established directly between OPNsense and an Azure VPN Gateway, connecting the on-premises `192.168.10.0/24` LAN with the Azure `10.0.0.0/16` network.

Private communication between a VMware workload and the Azure Windows Server at `10.0.1.4` was successfully validated across the tunnel.

The project provided hands-on experience configuring and troubleshooting routing, NAT, firewall policies, IPsec/IKEv2 negotiation, Azure networking, NSGs, Windows/Linux systems, and end-to-end hybrid connectivity.
