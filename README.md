# VLAN and Inter-VLAN Routing - Packet Tracer Project

This project demonstrates the configuration of VLANs and Inter-VLAN routing using Cisco Packet Tracer. The network consists of three units in a bookshop: Sales, Admin, and Customer, each having its own VLAN. Inter-VLAN routing is achieved through the "Router on a Stick" configuration. Below are the steps to set up the network:

## Network Topology
![Network Topology](https://github.com/yukwokto/Network-VLAN-Inter-VLAN/blob/cdf7ff7a580be85d3bf39301123e11878d6fadcd/pictures/Network_Topology.png)

### Initial Configuration

IP Address:
```
Sales-1	to 3     10.10.10.1, 2, 3/24
Admin-1	to 3     10.10.20.1, 2, 3/24
Customer-1 to 3  10.10.30.1 ,2 ,3/24
```

Default Gateway
```
Sales:     10.10.10.5
Admin:     10.10.20.5
Customer:  10.10.30.5
```

### Configuration Steps

Step 1: Enable Trunk Ports on L1/L2/L3/Core Switch

1. Connect to the switches or router through Cisco Packet Tracer's CLI.
2. Enter the following commands for each interface connecting two switches or the router in global configuration mode:
```
en
conf t
interface <port connecting 2 switches/ Router>
switchport mode trunk
```

Step 2: Configure VLAN Trunking Protocol on the Core Switch
```
Core-Switch(config)#vtp domain Ottawa_Bookshop
Core-Switch(config)#vtp mode server
Core-Switch(config)#vlan 10
Core-Switch(config-vlan)#name Sales
Core-Switch(config-vlan)#vlan 20
Core-Switch(config-vlan)#name Admin
Core-Switch(config-vlan)#vlan 30
Core-Switch(config-vlan)#name Customer
```

Verify correct vlan domain, mode, and password have been configured:
```
show vtp status
```
![show vtp status](https://github.com/yukwokto/Network-VLAN-Inter-VLAN/blob/fecc81277ac303a86357acdc3e71a4e7dbe63604/pictures/Core-Switch_sh_vtp_status.png)

Verify correct vlan have been configured:
```
show vlan brief
```
![show vlan brief](https://github.com/yukwokto/Network-VLAN-Inter-VLAN/blob/7fa8b59b8b3f03c0f4321e3e91e9f5a4d003cb2d/pictures/Core-Switch_sh_vlan_brief.png)


Step 3: Configure Access Ports on L1/L2/L3 Switches According to Their VLANs

```
L1/2/3-Switch(config)#int f0/1
L1/2/3-Switch(config-if)#switchport mode access 
L1/2/3-Switch(config-if)#switchport access vlan 10

L1/2/3-Switch(config)#int f0/2
L1/2/3-Switch(config-if)#switchport mode access
L1/2/3-Switch(config-if)#switchport access vlan 20

L1/2/3-Switch(config-if)#int f0/3
L1/2/3-Switch(config-if)#switchport mode access
L1/2/3-Switch(config-if)#switchport access vlan 30
```

Step 4: Configure Inter-VLAN Routing (Router on a Stick)

```
Router(config-if)#interface g0/0/0.10
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip address 10.10.10.5 255.255.255.0

Router(config-subif)#int g0/0/0.20
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip address 10.10.20.5 255.255.255.0

Router(config-subif)#int g0/0/0.30
Router(config-subif)#encapsulation dot1Q 30
Router(config-subif)#ip address 10.10.30.5 255.255.255.0
```

Step 5: Verify the connectivity between different VLANs

- Verify the connectivity between the Sales and Admin Unit
```
Sales-1> ping 10.10.20.1
```
![Sales-1> ping 10.10.20.1](https://github.com/yukwokto/Network-VLAN-Inter-VLAN/blob/c2956864a3adbcc4f0961aa9cda25cb93fe941f4/pictures/ping1.png)

- Verify the connectivity between the Sales and Customer Unit

```
Sales-1> ping 10.10.30.1
```
![Sales-1> ping 10.10.30.1](https://github.com/yukwokto/Network-VLAN-Inter-VLAN/blob/c2956864a3adbcc4f0961aa9cda25cb93fe941f4/pictures/ping2.png)

- Verify the connectivity between Admin and Customer Unit
```
Admin-1> ping 10.10.30.1
```
![Admin-1> ping 10.10.30.1](https://github.com/yukwokto/Network-VLAN-Inter-VLAN/blob/c2956864a3adbcc4f0961aa9cda25cb93fe941f4/pictures/ping3.png)


In conclusion, this network project successfully demonstrates the implementation of VLANs and Inter-VLAN routing using Cisco Packet Tracer. By segmenting the network into separate virtual LANs, I efficiently organized the departments—Sales, Admin, and Customer—enhancing security, manageability, and performance. The use of the "Router on a Stick" approach enabled communication between VLANs, allowing efficient data transfer across different departments. 

Through this project, I have showcased our ability to design and configure complex networking solutions, which are crucial in real-world scenarios to optimize network performance and ensure data security. This hands-on experience has undoubtedly honed our networking skills, enabling me to tackle more intricate networking challenges in the future.
