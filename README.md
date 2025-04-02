# Basic VLAN Setup Homelab

## Introduction
This project demonstrates how to configure a VLAN-based network using Cisco Packet Tracer. The goal was to segment network traffic into different VLANs, ensuring improved security and network efficiency. This setup included a **Layer 2 VLAN configuration** without a router, using a **core switch** and two **access switches** to manage VLAN communication.

To put it simply, the objective was to setup an office network with four VLANS: one for regular office staff, one for HR, one for IT, and one for VoIP devices like IP phones. The core switch connects two access switches in which I tested their connectivity.

## Summary of Steps
### 1. Set Up Network Topology
- Opened **Cisco Packet Tracer**.
- Added the following devices to the workspace:
  - **Core Switch (2960-24TT)**
  - **Access Switch0 and Access Switch1 (2960-24TT)**
  - **PC0, PC1, PC2, PC3, PC4** (Assigned to different VLANs)
  - **IP Phones for Voice VLAN**
 
![Network Topology](https://github.com/alytheanalyst/VLANHomelab/blob/main/settingitup.png?raw=true)

- Connected the devices:
  - **Core Switch to Access Switches**: Used **trunk links**.
      - Switch-0 to Switch-2 (e.g., GigabitEthernet 0/1 to GigabitEthernet 0/1).
      - Switch-1 to Switch-2 (e.g., GigabitEthernet 0/1 to GigabitEthernet 0/2).
  - **Access Switches to PCs and IP Phones**: Used **FastEthernet** cables.
     - PC-0 to Switch-0 (e.g., FastEthernet 0/1).
     - IP Phone 0 to Switch 0 (e.g., Switch to FastEthernet 0/2)
     - PC-1 to IP Phone 0. (e.g., PC to FastEthernet 0)
     - IP Phone 1 to Switch 0 (e.g., Switch to FastEthernet 0/6)
     - PC-2 to IP Phone 1. (e.g., PC to FastEthernet 0)
     - PC-3 to Switch-1 (e.g., FastEthernet 0/1).
     - PC-2 to Switch-1 (e.g., FastEthernet 0/2)
   
![Network Topology](https://github.com/alytheanalyst/VLANHomelab/blob/main/connecting.png?raw=true)

```yaml
# Image Placeholder for Network Topology
![Network Topology](https://github.com/alytheanalyst/VLANHomelab/blob/main/settingitup.png?raw=true)
```

### 2. Configure VLANs on Core and Access Switches
- Accessed each switch CLI and entered configuration mode.
- Created VLANs and assigned ports accordingly:


![Network Topology](https://github.com/alytheanalyst/VLANHomelab/blob/main/connecting.png?raw=true)


```yaml
# Image Placeholder for VLAN Configuration on Switch
![VLAN Config](path/to/vlan-config-image.png)
```

### 3. Configure Trunk Links Between Switches
- Set up trunk ports between the core switch and access switches to allow multiple VLANs to pass through.
- Configured trunk links using **dot1Q encapsulation**.

```yaml
# Image Placeholder for Trunk Configuration
![Trunk Config](path/to/trunk-config-image.png)
```

### 4. Test Connectivity
- Used `ping` between PCs in the same VLAN to verify intra-VLAN communication.
- Verified VLAN assignments with `show vlan brief`.
- Checked trunk link status using `show interfaces trunk`.

```yaml
# Image Placeholder for Ping Tests
![Ping Test](path/to/ping-test-image.png)
```

## Configuration Code
### CORE SWITCH CONFIGURATION
```
enable
configure terminal

# Create VLANs
vlan 10
name Office
vlan 20
name HR
vlan 30
name IT
vlan 40
name Voice
exit

# Configure trunk ports to access switches
interface FastEthernet 0/1
switchport mode trunk
exit

interface FastEthernet 0/2
switchport mode trunk
exit

# Save Configuration
write memory
```

### ACCESS SWITCH CONFIGURATION (Repeat for Both Access Switches)
```
enable
configure terminal

# Assign VLANs to Ports
interface FastEthernet 0/1
switchport mode access
switchport access vlan 10
exit

interface FastEthernet 0/2
switchport mode access
switchport access vlan 20
exit

interface FastEthernet 0/3
switchport mode access
switchport access vlan 30
exit

# Configure trunk link to core switch
interface FastEthernet 0/24
switchport mode trunk
exit

# Save Configuration
write memory
```

## What Was Learned
- **VLAN Segmentation**: How to create and assign VLANs to ports.
- **Trunking**: Allowing multiple VLANs over a single link between switches.
- **Layer 2 Switching**: Managing VLAN communication without a router.
- **Network Troubleshooting**: Using commands like `show vlan brief`, `ping`, and `show interfaces trunk` to diagnose network issues.

This homelab served as a **fundamental networking project** that showcased skills in VLAN setup, trunking, and troubleshooting.
