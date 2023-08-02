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

Verification the configuration using the following commands:
```
show vtp status
```
![show vtp status]()
```
show vlan brief
```
![show vlan brief]()














