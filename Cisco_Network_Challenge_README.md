# Cisco Network Configuration Exercise: Interface Setup, DHCP, and VLANs

## Purpose
Success Coach Challenges provide real-world IT practice in a structured environment.
This challenge focuses on configuring a functional Cisco network that includes:

- Router interface and subinterface configuration
- DHCP setup
- VLAN creation
- Switchport assignments
- Connectivity testing

These skills are essential for IT support, networking, and system administration roles.

---

## Challenge Title
**Cisco Network Configuration Exercise: Interface Setup, DHCP, and VLANs**

---

## Learning Objectives
1. Configure router and switch interfaces from scratch.
2. Create router subinterfaces for VLANs.
3. Enable DHCP to automatically assign IP addresses.
4. Build VLANs and assign ports on the switch.
5. Test and verify full network connectivity.

---

## On-the-Job Scenario
You recently joined an IT department that is upgrading its internal network.
Your task is to configure:

- A Cisco router  
- A Cisco switch  
- DHCP for automatic IP allocation  
- VLAN segmentation for different departments  

This challenge mirrors real responsibilities of a junior network technician.

---

# Challenge Steps

---

# 1. Configure Basic Router and Switch Interfaces

### Goal
Bring the interfaces online and prepare the router to communicate with VLANs.

### Steps
1. Open Cisco Packet Tracer.
2. Add the following devices:
   - 1 Router
   - 1 Switch
   - PCs
3. Connect them using straight-through cables.

### Router CLI Commands
```
enable
configure terminal
interface gigabitEthernet0/0
no shutdown
exit
```

---

# 2. Create Router Subinterfaces for VLANs

### Goal
Use router-on-a-stick by creating one subinterface per VLAN.

### Commands
```
! Subinterface for VLAN 10 (Marketing)
interface gigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit

! Subinterface for VLAN 20 (HR)
interface gigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
```

**Explanation:**  
- `.10` and `.20` are virtual interfaces.
- `encapsulation dot1Q` assigns each subinterface to its VLAN.
- Each subinterface acts as the default gateway for that VLAN.

---

# 3. Configure DHCP Services on the Router

### Goal
Allow PCs in VLAN 10 to automatically receive IP addresses.

### Commands
Exclude reserved IPs:
```
ip dhcp excluded-address 192.168.10.1 192.168.10.10
```

Create the DHCP pool:
```
ip dhcp pool VLAN10_Pool
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
exit
```

Check DHCP:
```
show ip dhcp pool
show ip dhcp binding
```

---

# 4. Create VLANs and Assign Ports on the Switch

### Goal
Separate traffic by department.

### Step 1 — Create VLANs
```
configure terminal
vlan 10
name Marketing
vlan 20
name HR
exit
```

### Step 2 — Assign Access Ports
```
! Marketing VLAN 10
interface range fa0/1 - 4
switchport mode access
switchport access vlan 10
exit

! HR VLAN 20
interface range fa0/5 - 8
switchport mode access
switchport access vlan 20
exit
```

### Step 3 — Configure Trunking
```
interface gigabitEthernet0/1
switchport mode trunk
switchport trunk allowed vlan 10,20
no shutdown
exit
```

---

# 5. Verify All Configurations

### Router Verification
```
show ip interface brief
```

Expected:
- Gi0/0.10 UP
- Gi0/0.20 UP

### Switch Verification
```
show vlan brief
show interfaces trunk
```

### Verify DHCP on the PC
1. Go to Desktop → IP Configuration
2. Select DHCP

Expected:
- IP: 192.168.10.x
- Gateway: 192.168.10.1
- DNS: 8.8.8.8

### Ping Test
```
ping 192.168.10.1
```

Successful replies confirm a working network.

---

# Screenshots to Include in GitHub
1. Basic router/switch setup
2. DHCP configuration
3. VLAN creation and port assignments
4. Router interface summary
5. Switch VLAN summary
6. PC receiving DHCP address
7. Successful ping
8. Final network topology

---

## Summary
This challenge teaches you how to build and verify a small Cisco network including:

- Router interfaces and subinterfaces
- DHCP setup
- VLAN creation
- Access and trunk port assignments
- Network testing and troubleshooting

These are key foundational networking skills used in real IT environments.
