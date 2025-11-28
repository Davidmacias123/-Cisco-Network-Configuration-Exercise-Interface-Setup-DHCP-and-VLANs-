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



<img width="1597" height="892" alt="image" src="https://github.com/user-attachments/assets/07d847cc-9586-4b1f-8ea3-475f21d1c8c8" />



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


<img width="1601" height="792" alt="image" src="https://github.com/user-attachments/assets/09308760-2da9-43d9-b309-defb6ca971e6" />

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
<img width="912" height="576" alt="image" src="https://github.com/user-attachments/assets/20b4300c-2ff6-4020-86a8-350eeee425e5" />

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
<img width="1706" height="842" alt="image" src="https://github.com/user-attachments/assets/436f6ef2-cac4-428c-8998-f51c6d4fce1f" />

---

# 5. Verify All Configurations

### Router Verification
```
show ip interface brief
```

Expected:
- Gi0/0.10 UP
- Gi0/0.20 UP

<img width="917" height="133" alt="image" src="https://github.com/user-attachments/assets/4bf91911-8d04-4dae-bedc-8893388d9833" />


### Switch Verification
```
show vlan brief
show interfaces trunk
```

<img width="921" height="482" alt="image" src="https://github.com/user-attachments/assets/21500408-82ff-4f6b-9b5d-d0c3b66bd836" />



### Verify DHCP on the PC
1. Go to Desktop → IP Configuration
2. Select DHCP

<img width="882" height="647" alt="image" src="https://github.com/user-attachments/assets/a13169de-6fe2-43aa-8fd5-7f34babc911f" />

---


Expected:
- IP: 192.168.10.x
- Gateway: 192.168.10.1
- DNS: 8.8.8.8

### Ping Test
```
ping 192.168.10.1
```

Successful replies confirm a working network.

<img width="853" height="357" alt="image" src="https://github.com/user-attachments/assets/5ede3163-e019-4ede-a185-bb65a8250685" />


---

## Summary
This challenge teaches you how to build and verify a small Cisco network including:

- Router interfaces and subinterfaces
- DHCP setup
- VLAN creation
- Access and trunk port assignments
- Network testing and troubleshooting

These are key foundational networking skills used in real IT environments.
