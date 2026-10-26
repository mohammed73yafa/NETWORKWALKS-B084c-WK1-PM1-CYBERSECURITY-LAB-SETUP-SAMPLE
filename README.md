# NETWORKWALKS-B082-WK1-PM1-CYBERSECURITY-LAB-SETUP-SAMPLE

# Cybersecurity Lab Environment Setup

Building an isolated virtual lab for penetration testing and ethical hacking practice.

## Project Overview

This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using VMware and Kali Linux. 

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely.

The lab is configured on a private virtual network so that additional target machines can be integrated later for authorized security testing practice.

## Objectives

- Setup and configure the virtualization platform (VMware).
- Import and configure Kali Linux as the primary attacking machine.
- Create a private NAT network segment for the lab environment.
- Configure network connectivity and static IPv4 addressing.
- Verify connectivity, gateway access, and network routing.
- Document the complete setup process.

## Lab Configuration

| Component | Configuration |
| :--- | :--- |
| Host OS | Windows |
| Hypervisor | VMware Workstation |
| Security OS | Kali Linux |
| Virtual Network | NAT / VMnet10 |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

## Lab Setup Procedure

### Step 1. Virtual Network Configuration
A dedicated custom NAT network (VMnet10) was configured in VMware using the subnet `10.0.0.0/24` to allow internal communication and outbound connectivity for lab machines.

### Step 2. Kali Linux Import & Network Attachment
Kali Linux was imported into VMware, and its network adapter was attached to the custom NAT network segment.

### Step 3. Static IP Configuration
The Kali Linux network interface was configured manually with a static IPv4 address to ensure consistency across future lab exercises:
- IP Address: `10.0.0.2`
- Subnet Mask: `255.255.255.0`
- Gateway: `10.0.0.1`
- DNS: `8.8.8.8`

## Lab Verification

- **IP Verification:** Confirmed via `ip a` that the interface holds `10.0.0.2/24`.
- **Gateway Ping:** Successfully tested connectivity to `10.0.0.1` with zero packet loss.

## Problems Encountered & Solutions

### Problem 1: Static IP Address Activation in NetworkManager
After applying static IPv4 settings, the connection interface occasionally required resetting due to duplicate address detection delays in Linux.

**Solution:**
Executed the following commands in the terminal to update connection parameters and restart the interface:
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
