# Cybersecurity Testing Lab Setup: Kali Linux on VirtualBox

A virtual cybersecurity lab with a Kali Linux attacker machine on a private VirtualBox NAT Network (10.0.0.0/24), built for ethical hacking practice.

Completed as the Week 1 project of the Networkwalks Cybersecurity program (Batch B084).

## Tools used
- Windows (host OS)
- Oracle VirtualBox
- Kali Linux (pre-built VirtualBox image)
- 7-Zip

## Lab details
- Network: NatNetwork, 10.0.0.0/24, DHCP enabled
- Kali Linux IP: 10.0.0.2/24
- Gateway: 10.0.0.1
- DNS: 8.8.8.8
- Shared clipboard and drag-and-drop: Bidirectional
- Shared folder: Windows Downloads folder

## Steps

### 1. Installed VirtualBox and created the NAT Network
Created a NAT Network named NatNetwork with the prefix 10.0.0.0/24.

![NAT Network](01-nat-network.png)

### 2. Imported Kali Linux
Extracted the Kali VirtualBox image with 7-Zip and added the .vbox file to VirtualBox.

### 3. Configured the VM settings
Attached Adapter 1 to NAT Network, enabled the clipboard and drag-and-drop, and added the shared folder.

![Kali network settings](02-kali-network-settings.png)

### 4. Set the static IP on Kali
Set the IP to 10.0.0.2/24 with gateway 10.0.0.1 and DNS 8.8.8.8.

### 5. Tested connectivity
Pinged the gateway and an external domain to confirm network access and DNS resolution.

![Ping test](03-ping-test.png)

### 6. Took a VM snapshot
Created a clean snapshot for recovery.

![Snapshot](04-snapshot.png)

## Problem solved
The Kali VM kept losing its network connection. I fixed it by disabling duplicate address detection on the connection:

    sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
    sudo nmcli connection down "Wired connection 1"
    sudo nmcli connection up "Wired connection 1"

## What I learned
- Virtual machine networking and how a NAT Network differs from plain NAT
- Static IP configuration with NetworkManager
- Troubleshooting network drops
- Using snapshots for recovery
- Documenting technical work

## Note
This lab is for learning and authorized testing only.
