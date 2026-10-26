<div align="center">

# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-VMware%20Workstation-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Muhammad%20Sami-C00000?style=flat-square" />
</p>

---

## 📌 Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using VMware Workstation and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

---

## 🎯 Objectives

The main objectives of this project are to:

- Configure VMware Workstation virtual networking (VMnet custom NAT).
- Import and configure Kali Linux as a virtual machine.
- Create a private **NAT Network segment** (`10.0.0.0/24`) for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent static IP address (`10.0.0.2`) to the Kali VM.
- Verify network connectivity, gateway access, and interface states.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation



---

## 🏗️ Lab Architecture

![](1-screenshot-title-image.png)

Additional target machines can be added to the same virtual network in future projects.

---

## ⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------- |
| 🖥️ Host OS         | Windows             |
| 🧠 Host RAM        | 8 GB                |
| ⚡ Hypervisor      | VMware Workstation  |
| 🐉 Security OS     | Kali Linux 2026.2   |
| 🧠 Kali RAM        | 2048 MB             |
| 🌐 Virtual Network | Custom NAT (VMnet10)|
| 📡 Network Address | 10.0.0.0/24         |
| 🐧 Kali IP Address | 10.0.0.2/24         |
| 🚪 Default Gateway | 10.0.0.1            |
| 🌍 DNS Server      | 8.8.8.8             |
| 🔮 Future VM Range | 10.0.0.3–10.0.0.99  |

---

# 🪜 Lab Setup Procedure

## Step 1. Hypervisor Setup (VMware Workstation)

VMware Workstation was selected as the virtualization platform to host the cybersecurity laboratory.

---

## Step 2. Create the Custom NAT Network

A dedicated custom NAT network segment (`VMnet10`) was configured in VMware Virtual Network Editor.

Configuration:
- **Network Name:** VMnet10 (NAT)
- **Subnet IP:** 10.0.0.0
- **Subnet Mask:** 255.255.255.0
- **DHCP:** Enabled

![](2-screenshot-network-settings-1.png)

A **NAT Network segment** was chosen because virtual machines connected to it can communicate locally while routing outbound traffic securely through the host connection.

---

## Step 3. Import Kali Linux

Kali Linux was imported into VMware Workstation, and the virtual machine network adapter was assigned to the custom NAT network.

The VM network adapter was configured as follows:

```text
Network Connection: Custom: Specific virtual network -> VMnet10 (NAT)

```

The VM was allocated:

```text
RAM: 2048 MB

```
![](3-screenshot-kali-linux.png)
---

## Step 4. Configure the Kali Linux Network

The Kali Linux network interface was configured manually with a static IPv4 address to ensure stability and consistency across lab exercises.

Configuration:

```text
IP Address: 10.0.0.2
Subnet Mask: 255.255.255.0 (Prefix /24)
Gateway: 10.0.0.1
DNS: 8.8.8.8

```
![](4-screenshot-kali-network-settings.png)
---

# 🔎 Lab Verification

| ✅ Test | 🧾 Command | 🎯 Expected Result |
| --- | --- | --- |
| 🌐 Check IP address | `ip a` | Correct Kali IP (`10.0.0.2`) |
| 📡 Test gateway | `ping 10.0.0.1` | Successful replies (0% loss) |
| 🌍 Test Internet connectivity | `ping 8.8.8.8` | Successful packet routing |

### Example Results

```text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8

```

---

# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

## Problem 1. Static IP Address Activation in NetworkManager

After manually applying static IPv4 settings in Linux, network interface states can occasionally experience duplicate address detection delays or fail to activate cleanly.

Solution applied:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"

```

The network connection was successfully restarted and verified.

> **Important:** Network interface and connection names may differ between systems. Verify your actual connection name before executing `nmcli` commands.

---

# 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

### 1. Custom NAT Virtual Networks

Configuring custom virtual switches and network segments (`VMnet`) to isolate lab traffic while allowing controlled routing.

### 2. Virtual Machine Networking

Understanding how hypervisor network adapters attach virtual machines to designated subnets and affect internal communication.

### 3. Static IP Configuration

Configuring and verifying static IPv4 parameters, subnet masks, and gateways in Linux distributions.

### 4. Troubleshooting Network Interfaces

Resolving network manager states and interface activation parameters using command-line administration tools.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for education purposes only.

---

# 🔗 Tools & Resources

* **VMware Workstation:** [https://www.vmware.com](https://www.vmware.com)
* **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)

---

# 👤 Author

**Muhammad Sami **

Cybersecurity Student

---

## 📌 Project Information

**Program Name:** Cybersecurity Training | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub

```

```
