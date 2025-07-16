# FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| FABRIC | l3leaf | pod1-leaf-1 | 192.168.0.11/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod1-leaf-2 | 192.168.0.12/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod1-leaf-3 | 192.168.0.13/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod1-leaf-4 | 192.168.0.14/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod1-spine-1 | 192.168.0.101/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod1-spine-2 | 192.168.0.102/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod2-leaf-1 | 192.168.0.15/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod2-leaf-2 | 192.168.0.16/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod2-leaf-3 | 192.168.0.17/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod2-leaf-4 | 192.168.0.18/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod2-spine-1 | 192.168.0.103/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod2-spine-2 | 192.168.0.104/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod3-leaf-1 | 192.168.0.19/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod3-leaf-2 | 192.168.0.20/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod3-leaf-3 | 192.168.0.21/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod3-leaf-4 | 192.168.0.22/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod3-spine-1 | 192.168.0.105/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod3-spine-2 | 192.168.0.106/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod4-leaf-1 | 192.168.0.23/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod4-leaf-2 | 192.168.0.24/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod4-leaf-3 | 192.168.0.25/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | pod4-leaf-4 | 192.168.0.26/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod4-spine-1 | 192.168.0.107/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod4-spine-2 | 192.168.0.108/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | services-leaf-1 | 192.168.0.61/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | services-leaf-2 | 192.168.0.62/24 | vEOS-lab | Provisioned | - |
| FABRIC | super-spine | super-spine-1 | 192.168.0.1/24 | vEOS-lab | Provisioned | - |
| FABRIC | super-spine | super-spine-2 | 192.168.0.2/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | pod1-leaf-1 | Ethernet1 | spine | pod1-spine-1 | Ethernet3 |
| l3leaf | pod1-leaf-1 | Ethernet2 | spine | pod1-spine-2 | Ethernet3 |
| l3leaf | pod1-leaf-1 | Ethernet49 | mlag_peer | pod1-leaf-2 | Ethernet49 |
| l3leaf | pod1-leaf-1 | Ethernet50 | mlag_peer | pod1-leaf-2 | Ethernet50 |
| l3leaf | pod1-leaf-2 | Ethernet1 | spine | pod1-spine-1 | Ethernet4 |
| l3leaf | pod1-leaf-2 | Ethernet2 | spine | pod1-spine-2 | Ethernet4 |
| l3leaf | pod1-leaf-3 | Ethernet1 | spine | pod1-spine-1 | Ethernet5 |
| l3leaf | pod1-leaf-3 | Ethernet2 | spine | pod1-spine-2 | Ethernet5 |
| l3leaf | pod1-leaf-3 | Ethernet49 | mlag_peer | pod1-leaf-4 | Ethernet49 |
| l3leaf | pod1-leaf-3 | Ethernet50 | mlag_peer | pod1-leaf-4 | Ethernet50 |
| l3leaf | pod1-leaf-4 | Ethernet1 | spine | pod1-spine-1 | Ethernet6 |
| l3leaf | pod1-leaf-4 | Ethernet2 | spine | pod1-spine-2 | Ethernet6 |
| spine | pod1-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet1 |
| spine | pod1-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet1 |
| spine | pod1-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet2 |
| spine | pod1-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet2 |
| l3leaf | pod2-leaf-1 | Ethernet1 | spine | pod2-spine-1 | Ethernet7 |
| l3leaf | pod2-leaf-1 | Ethernet2 | spine | pod2-spine-2 | Ethernet7 |
| l3leaf | pod2-leaf-1 | Ethernet49 | mlag_peer | pod2-leaf-2 | Ethernet49 |
| l3leaf | pod2-leaf-1 | Ethernet50 | mlag_peer | pod2-leaf-2 | Ethernet50 |
| l3leaf | pod2-leaf-2 | Ethernet1 | spine | pod2-spine-1 | Ethernet8 |
| l3leaf | pod2-leaf-2 | Ethernet2 | spine | pod2-spine-2 | Ethernet8 |
| l3leaf | pod2-leaf-3 | Ethernet1 | spine | pod2-spine-1 | Ethernet9 |
| l3leaf | pod2-leaf-3 | Ethernet2 | spine | pod2-spine-2 | Ethernet9 |
| l3leaf | pod2-leaf-3 | Ethernet49 | mlag_peer | pod2-leaf-4 | Ethernet49 |
| l3leaf | pod2-leaf-3 | Ethernet50 | mlag_peer | pod2-leaf-4 | Ethernet50 |
| l3leaf | pod2-leaf-4 | Ethernet1 | spine | pod2-spine-1 | Ethernet10 |
| l3leaf | pod2-leaf-4 | Ethernet2 | spine | pod2-spine-2 | Ethernet10 |
| spine | pod2-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet3 |
| spine | pod2-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet3 |
| spine | pod2-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet4 |
| spine | pod2-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet4 |
| l3leaf | pod3-leaf-1 | Ethernet1 | spine | pod3-spine-1 | Ethernet11 |
| l3leaf | pod3-leaf-1 | Ethernet2 | spine | pod3-spine-2 | Ethernet11 |
| l3leaf | pod3-leaf-1 | Ethernet49 | mlag_peer | pod3-leaf-2 | Ethernet49 |
| l3leaf | pod3-leaf-1 | Ethernet50 | mlag_peer | pod3-leaf-2 | Ethernet50 |
| l3leaf | pod3-leaf-2 | Ethernet1 | spine | pod3-spine-1 | Ethernet12 |
| l3leaf | pod3-leaf-2 | Ethernet2 | spine | pod3-spine-2 | Ethernet12 |
| l3leaf | pod3-leaf-3 | Ethernet1 | spine | pod3-spine-1 | Ethernet13 |
| l3leaf | pod3-leaf-3 | Ethernet2 | spine | pod3-spine-2 | Ethernet13 |
| l3leaf | pod3-leaf-3 | Ethernet49 | mlag_peer | pod3-leaf-4 | Ethernet49 |
| l3leaf | pod3-leaf-3 | Ethernet50 | mlag_peer | pod3-leaf-4 | Ethernet50 |
| l3leaf | pod3-leaf-4 | Ethernet1 | spine | pod3-spine-1 | Ethernet14 |
| l3leaf | pod3-leaf-4 | Ethernet2 | spine | pod3-spine-2 | Ethernet14 |
| spine | pod3-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet5 |
| spine | pod3-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet5 |
| spine | pod3-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet6 |
| spine | pod3-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet6 |
| l3leaf | pod4-leaf-1 | Ethernet1 | spine | pod4-spine-1 | Ethernet15 |
| l3leaf | pod4-leaf-1 | Ethernet2 | spine | pod4-spine-2 | Ethernet15 |
| l3leaf | pod4-leaf-1 | Ethernet49 | mlag_peer | pod4-leaf-2 | Ethernet49 |
| l3leaf | pod4-leaf-1 | Ethernet50 | mlag_peer | pod4-leaf-2 | Ethernet50 |
| l3leaf | pod4-leaf-2 | Ethernet1 | spine | pod4-spine-1 | Ethernet16 |
| l3leaf | pod4-leaf-2 | Ethernet2 | spine | pod4-spine-2 | Ethernet16 |
| l3leaf | pod4-leaf-3 | Ethernet1 | spine | pod4-spine-1 | Ethernet17 |
| l3leaf | pod4-leaf-3 | Ethernet2 | spine | pod4-spine-2 | Ethernet17 |
| l3leaf | pod4-leaf-3 | Ethernet49 | mlag_peer | pod4-leaf-4 | Ethernet49 |
| l3leaf | pod4-leaf-3 | Ethernet50 | mlag_peer | pod4-leaf-4 | Ethernet50 |
| l3leaf | pod4-leaf-4 | Ethernet1 | spine | pod4-spine-1 | Ethernet18 |
| l3leaf | pod4-leaf-4 | Ethernet2 | spine | pod4-spine-2 | Ethernet18 |
| spine | pod4-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet7 |
| spine | pod4-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet7 |
| spine | pod4-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet8 |
| spine | pod4-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet8 |
| l3leaf | services-leaf-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet17 |
| l3leaf | services-leaf-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet17 |
| l3leaf | services-leaf-1 | Ethernet49 | mlag_peer | services-leaf-2 | Ethernet49 |
| l3leaf | services-leaf-1 | Ethernet50 | mlag_peer | services-leaf-2 | Ethernet50 |
| l3leaf | services-leaf-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet18 |
| l3leaf | services-leaf-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet18 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 10.255.250.0/24 | 256 | 32 | 12.5 % |
| 10.255.251.0/24 | 256 | 8 | 3.13 % |
| 10.255.252.0/24 | 256 | 16 | 6.25 % |
| 10.255.253.0/24 | 256 | 16 | 6.25 % |
| 10.255.254.0/24 | 256 | 16 | 6.25 % |
| 10.255.255.0/24 | 256 | 16 | 6.25 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| pod1-leaf-1 | Ethernet1 | 10.255.255.1/31 | pod1-spine-1 | Ethernet3 | 10.255.255.0/31 |
| pod1-leaf-1 | Ethernet2 | 10.255.255.3/31 | pod1-spine-2 | Ethernet3 | 10.255.255.2/31 |
| pod1-leaf-2 | Ethernet1 | 10.255.255.5/31 | pod1-spine-1 | Ethernet4 | 10.255.255.4/31 |
| pod1-leaf-2 | Ethernet2 | 10.255.255.7/31 | pod1-spine-2 | Ethernet4 | 10.255.255.6/31 |
| pod1-leaf-3 | Ethernet1 | 10.255.255.9/31 | pod1-spine-1 | Ethernet5 | 10.255.255.8/31 |
| pod1-leaf-3 | Ethernet2 | 10.255.255.11/31 | pod1-spine-2 | Ethernet5 | 10.255.255.10/31 |
| pod1-leaf-4 | Ethernet1 | 10.255.255.13/31 | pod1-spine-1 | Ethernet6 | 10.255.255.12/31 |
| pod1-leaf-4 | Ethernet2 | 10.255.255.15/31 | pod1-spine-2 | Ethernet6 | 10.255.255.14/31 |
| pod1-spine-1 | Ethernet1 | 10.255.250.1/31 | super-spine-1 | Ethernet1 | 10.255.250.0/31 |
| pod1-spine-1 | Ethernet2 | 10.255.250.3/31 | super-spine-2 | Ethernet1 | 10.255.250.2/31 |
| pod1-spine-2 | Ethernet1 | 10.255.250.5/31 | super-spine-1 | Ethernet2 | 10.255.250.4/31 |
| pod1-spine-2 | Ethernet2 | 10.255.250.7/31 | super-spine-2 | Ethernet2 | 10.255.250.6/31 |
| pod2-leaf-1 | Ethernet1 | 10.255.254.17/31 | pod2-spine-1 | Ethernet7 | 10.255.254.16/31 |
| pod2-leaf-1 | Ethernet2 | 10.255.254.19/31 | pod2-spine-2 | Ethernet7 | 10.255.254.18/31 |
| pod2-leaf-2 | Ethernet1 | 10.255.254.21/31 | pod2-spine-1 | Ethernet8 | 10.255.254.20/31 |
| pod2-leaf-2 | Ethernet2 | 10.255.254.23/31 | pod2-spine-2 | Ethernet8 | 10.255.254.22/31 |
| pod2-leaf-3 | Ethernet1 | 10.255.254.25/31 | pod2-spine-1 | Ethernet9 | 10.255.254.24/31 |
| pod2-leaf-3 | Ethernet2 | 10.255.254.27/31 | pod2-spine-2 | Ethernet9 | 10.255.254.26/31 |
| pod2-leaf-4 | Ethernet1 | 10.255.254.29/31 | pod2-spine-1 | Ethernet10 | 10.255.254.28/31 |
| pod2-leaf-4 | Ethernet2 | 10.255.254.31/31 | pod2-spine-2 | Ethernet10 | 10.255.254.30/31 |
| pod2-spine-1 | Ethernet1 | 10.255.250.9/31 | super-spine-1 | Ethernet3 | 10.255.250.8/31 |
| pod2-spine-1 | Ethernet2 | 10.255.250.11/31 | super-spine-2 | Ethernet3 | 10.255.250.10/31 |
| pod2-spine-2 | Ethernet1 | 10.255.250.13/31 | super-spine-1 | Ethernet4 | 10.255.250.12/31 |
| pod2-spine-2 | Ethernet2 | 10.255.250.15/31 | super-spine-2 | Ethernet4 | 10.255.250.14/31 |
| pod3-leaf-1 | Ethernet1 | 10.255.253.33/31 | pod3-spine-1 | Ethernet11 | 10.255.253.32/31 |
| pod3-leaf-1 | Ethernet2 | 10.255.253.35/31 | pod3-spine-2 | Ethernet11 | 10.255.253.34/31 |
| pod3-leaf-2 | Ethernet1 | 10.255.253.37/31 | pod3-spine-1 | Ethernet12 | 10.255.253.36/31 |
| pod3-leaf-2 | Ethernet2 | 10.255.253.39/31 | pod3-spine-2 | Ethernet12 | 10.255.253.38/31 |
| pod3-leaf-3 | Ethernet1 | 10.255.253.41/31 | pod3-spine-1 | Ethernet13 | 10.255.253.40/31 |
| pod3-leaf-3 | Ethernet2 | 10.255.253.43/31 | pod3-spine-2 | Ethernet13 | 10.255.253.42/31 |
| pod3-leaf-4 | Ethernet1 | 10.255.253.45/31 | pod3-spine-1 | Ethernet14 | 10.255.253.44/31 |
| pod3-leaf-4 | Ethernet2 | 10.255.253.47/31 | pod3-spine-2 | Ethernet14 | 10.255.253.46/31 |
| pod3-spine-1 | Ethernet1 | 10.255.250.17/31 | super-spine-1 | Ethernet5 | 10.255.250.16/31 |
| pod3-spine-1 | Ethernet2 | 10.255.250.19/31 | super-spine-2 | Ethernet5 | 10.255.250.18/31 |
| pod3-spine-2 | Ethernet1 | 10.255.250.21/31 | super-spine-1 | Ethernet6 | 10.255.250.20/31 |
| pod3-spine-2 | Ethernet2 | 10.255.250.23/31 | super-spine-2 | Ethernet6 | 10.255.250.22/31 |
| pod4-leaf-1 | Ethernet1 | 10.255.252.49/31 | pod4-spine-1 | Ethernet15 | 10.255.252.48/31 |
| pod4-leaf-1 | Ethernet2 | 10.255.252.51/31 | pod4-spine-2 | Ethernet15 | 10.255.252.50/31 |
| pod4-leaf-2 | Ethernet1 | 10.255.252.53/31 | pod4-spine-1 | Ethernet16 | 10.255.252.52/31 |
| pod4-leaf-2 | Ethernet2 | 10.255.252.55/31 | pod4-spine-2 | Ethernet16 | 10.255.252.54/31 |
| pod4-leaf-3 | Ethernet1 | 10.255.252.57/31 | pod4-spine-1 | Ethernet17 | 10.255.252.56/31 |
| pod4-leaf-3 | Ethernet2 | 10.255.252.59/31 | pod4-spine-2 | Ethernet17 | 10.255.252.58/31 |
| pod4-leaf-4 | Ethernet1 | 10.255.252.61/31 | pod4-spine-1 | Ethernet18 | 10.255.252.60/31 |
| pod4-leaf-4 | Ethernet2 | 10.255.252.63/31 | pod4-spine-2 | Ethernet18 | 10.255.252.62/31 |
| pod4-spine-1 | Ethernet1 | 10.255.250.25/31 | super-spine-1 | Ethernet7 | 10.255.250.24/31 |
| pod4-spine-1 | Ethernet2 | 10.255.250.27/31 | super-spine-2 | Ethernet7 | 10.255.250.26/31 |
| pod4-spine-2 | Ethernet1 | 10.255.250.29/31 | super-spine-1 | Ethernet8 | 10.255.250.28/31 |
| pod4-spine-2 | Ethernet2 | 10.255.250.31/31 | super-spine-2 | Ethernet8 | 10.255.250.30/31 |
| services-leaf-1 | Ethernet1 | 10.255.251.65/31 | super-spine-1 | Ethernet17 | 10.255.251.64/31 |
| services-leaf-1 | Ethernet2 | 10.255.251.67/31 | super-spine-2 | Ethernet17 | 10.255.251.66/31 |
| services-leaf-2 | Ethernet1 | 10.255.251.69/31 | super-spine-1 | Ethernet18 | 10.255.251.68/31 |
| services-leaf-2 | Ethernet2 | 10.255.251.71/31 | super-spine-2 | Ethernet18 | 10.255.251.70/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 100.100.0.0/26 | 64 | 4 | 6.25 % |
| 100.100.0.64/26 | 64 | 4 | 6.25 % |
| 100.100.0.128/26 | 64 | 4 | 6.25 % |
| 100.100.0.192/26 | 64 | 4 | 6.25 % |
| 100.101.0.0/26 | 64 | 2 | 3.13 % |
| 100.103.0.0/26 | 64 | 2 | 3.13 % |
| 100.104.0.0/26 | 64 | 8 | 12.5 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | pod1-leaf-1 | 100.100.0.1/32 |
| FABRIC | pod1-leaf-2 | 100.100.0.2/32 |
| FABRIC | pod1-leaf-3 | 100.100.0.3/32 |
| FABRIC | pod1-leaf-4 | 100.100.0.4/32 |
| FABRIC | pod1-spine-1 | 100.104.0.1/32 |
| FABRIC | pod1-spine-2 | 100.104.0.2/32 |
| FABRIC | pod2-leaf-1 | 100.100.0.71/32 |
| FABRIC | pod2-leaf-2 | 100.100.0.72/32 |
| FABRIC | pod2-leaf-3 | 100.100.0.73/32 |
| FABRIC | pod2-leaf-4 | 100.100.0.74/32 |
| FABRIC | pod2-spine-1 | 100.104.0.3/32 |
| FABRIC | pod2-spine-2 | 100.104.0.4/32 |
| FABRIC | pod3-leaf-1 | 100.100.0.139/32 |
| FABRIC | pod3-leaf-2 | 100.100.0.140/32 |
| FABRIC | pod3-leaf-3 | 100.100.0.141/32 |
| FABRIC | pod3-leaf-4 | 100.100.0.142/32 |
| FABRIC | pod3-spine-1 | 100.104.0.5/32 |
| FABRIC | pod3-spine-2 | 100.104.0.6/32 |
| FABRIC | pod4-leaf-1 | 100.100.0.207/32 |
| FABRIC | pod4-leaf-2 | 100.100.0.208/32 |
| FABRIC | pod4-leaf-3 | 100.100.0.209/32 |
| FABRIC | pod4-leaf-4 | 100.100.0.210/32 |
| FABRIC | pod4-spine-1 | 100.104.0.7/32 |
| FABRIC | pod4-spine-2 | 100.104.0.8/32 |
| FABRIC | services-leaf-1 | 100.101.0.17/32 |
| FABRIC | services-leaf-2 | 100.101.0.18/32 |
| FABRIC | super-spine-1 | 100.103.0.1/32 |
| FABRIC | super-spine-2 | 100.103.0.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |
| 10.100.1.0/26 | 64 | 6 | 9.38 % |
| 10.100.1.64/26 | 64 | 4 | 6.25 % |
| 10.100.1.128/26 | 64 | 4 | 6.25 % |
| 10.100.1.192/26 | 64 | 4 | 6.25 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | pod1-leaf-1 | 10.100.1.1/32 |
| FABRIC | pod1-leaf-2 | 10.100.1.1/32 |
| FABRIC | pod1-leaf-3 | 10.100.1.3/32 |
| FABRIC | pod1-leaf-4 | 10.100.1.3/32 |
| FABRIC | pod2-leaf-1 | 10.100.1.71/32 |
| FABRIC | pod2-leaf-2 | 10.100.1.71/32 |
| FABRIC | pod2-leaf-3 | 10.100.1.73/32 |
| FABRIC | pod2-leaf-4 | 10.100.1.73/32 |
| FABRIC | pod3-leaf-1 | 10.100.1.139/32 |
| FABRIC | pod3-leaf-2 | 10.100.1.139/32 |
| FABRIC | pod3-leaf-3 | 10.100.1.141/32 |
| FABRIC | pod3-leaf-4 | 10.100.1.141/32 |
| FABRIC | pod4-leaf-1 | 10.100.1.207/32 |
| FABRIC | pod4-leaf-2 | 10.100.1.207/32 |
| FABRIC | pod4-leaf-3 | 10.100.1.209/32 |
| FABRIC | pod4-leaf-4 | 10.100.1.209/32 |
| FABRIC | services-leaf-1 | 10.100.1.17/32 |
| FABRIC | services-leaf-2 | 10.100.1.17/32 |
