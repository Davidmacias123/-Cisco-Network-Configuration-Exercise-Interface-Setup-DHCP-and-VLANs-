# Cisco Network Configuration Exercise: Interface Setup, DHCP, and VLANs

## Purpose
Success Coach Challenges allow each learner to experience real-world IT operations in a guided environment supported by RapidAscent’s Coaching team. This challenge focuses on hands-on Cisco router and switch configuration to build confidence in network setup and troubleshooting.

## Challenge Title
**Cisco Network Configuration Exercise: Interface Setup, DHCP, and VLANs**

## Learning Objectives
1. Configure the initial router and switch interfaces.  
2. Set up DHCP services to dynamically assign IP addresses.  
3. Implement VLANs for network segmentation.  
4. Develop problem‑solving skills for IP network design and testing.

## On-the-Job Scenario
You have joined the IT department of a mid-sized company upgrading its network. Your task is to configure a Cisco router and switch to support dynamic IP allocation and VLAN segmentation for different departments.

---

# Challenge Steps

---

# 1. Configure Basic Router and Switch Interfaces

### What You Are Doing
Building the foundation of your network by giving your router and switch interfaces IP addresses and enabling connections.

### Steps
1. Open **Cisco Packet Tracer** and start a new project.  
2. Add a **Router**, **Switch**, and **PCs**.  
3. Use the correct cables:  
   - Straight-through = Different devices  
   - Crossover = Similar devices  
4. Open the router CLI:  
   ```
   enable
   configure terminal
   interface gigabitEthernet0/0
   no shutdown
   ```
5. Assign the interface its IP:
   ```
   ip address 192.168.1.1 255.255.255.0
   ```

---

# 2. Enable DHCP on the Router

### What You Are Doing
Creating a DHCP service that automatically hands out IP addresses to devices.

### Commands
Enter configuration mode:
```
configure terminal
```

Exclude addresses you don’t want DHCP to use:
```
ip dhcp excluded-address 192.168.10.1 192.168.10.10
```

Create the DHCP pool:
```
ip dhcp pool VLAN10_Pool
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
```

Verify DHCP:
```
show ip dhcp binding
show ip dhcp pool
```

---

# 3. Create VLANs and Assign Ports on the Switch

### What You Are Doing
Separating departments into different virtual networks.

### Commands
Enter switch configuration:
```
configure terminal
```

Create VLANs:
```
vlan 10
name Marketing
vlan 20
name HR
```

Assign switch ports:
```
interface range fa0/1 - 4
switchport mode access
switchport access vlan 10

interface range fa0/5 - 8
switchport mode access
switchport access vlan 20
```

Configure trunk for inter‑VLAN traffic:
```
interface gigabitEthernet0/1
switchport mode trunk
switchport trunk allowed vlan 10,20
no shutdown
```

---

# 4. Verify All Network Configurations

### Router Interfaces
```
show ip interface brief
```

### Switch VLANs
```
show vlan brief
show interfaces trunk
```

### Test DHCP on a PC
Set PC to **DHCP** and confirm it receives:  
- IP in 192.168.10.x  
- Gateway 192.168.10.1  
- DNS 8.8.8.8  

### Test Connectivity
Ping the gateway:
```
ping 192.168.10.1
```

Ping within the same VLAN or across VLANs if inter‑VLAN routing is configured.

---

# Network Topology (Screenshot Reference)

*(Images correspond to the steps in your challenge and should be uploaded to your GitHub repo for clarity.)*

---

# Summary
This challenge teaches foundational networking tasks:

- Router interface configuration  
- DHCP setup and verification  
- VLAN creation and port assignments  
- Trunking for VLAN communication  
- Device connectivity testing  

These skills are essential for IT support, networking, and system administration roles.

---

# Screenshots to Upload
1. Basic interface configuration  
2. DHCP configuration  
3. VLAN and port assignments  
4. Router interface table  
5. Switch VLAN table  
6. DHCP success on PC  
7. Ping results  
8. Final topology view  

---

This README.md explains every step in a simple and clear way so beginners can follow and learn effectively.
