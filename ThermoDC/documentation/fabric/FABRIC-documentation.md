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
| POD1_LEAFS | l3leaf | pod1-leaf-1 | 192.168.0.11/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-2 | 192.168.0.12/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-3 | 192.168.0.13/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-4 | 192.168.0.14/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-5 | 192.168.0.15/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-6 | 192.168.0.16/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-7 | 192.168.0.17/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-8 | 192.168.0.18/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-9 | 192.168.0.19/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-10 | 192.168.0.20/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-11 | 192.168.0.21/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-12 | 192.168.0.22/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-13 | 192.168.0.23/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-14 | 192.168.0.24/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-15 | 192.168.0.25/24 | vEOS-lab | Provisioned | - |
| POD1_LEAFS | l3leaf | pod1-leaf-16 | 192.168.0.26/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod1-spine-1 | 192.168.0.201/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod1-spine-2 | 192.168.0.202/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-1 | 192.168.0.43/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-2 | 192.168.0.44/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-3 | 192.168.0.45/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-4 | 192.168.0.46/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-5 | 192.168.0.47/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-6 | 192.168.0.48/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-7 | 192.168.0.49/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-8 | 192.168.0.50/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-9 | 192.168.0.51/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-10 | 192.168.0.52/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-11 | 192.168.0.53/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-12 | 192.168.0.54/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-13 | 192.168.0.55/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-14 | 192.168.0.56/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-15 | 192.168.0.57/24 | vEOS-lab | Provisioned | - |
| POD2_LEAFS | l3leaf | pod2-leaf-16 | 192.168.0.58/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod2-spine-1 | 192.168.0.203/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod2-spine-2 | 192.168.0.204/24 | vEOS-lab | Provisioned | - |
| POD3_LEAFS | l3leaf | pod3-leaf-1 | 192.168.0.75/24 | vEOS-lab | Provisioned | - |
| POD3_LEAFS | l3leaf | pod3-leaf-2 | 192.168.0.76/24 | vEOS-lab | Provisioned | - |
| POD3_LEAFS | l3leaf | pod3-leaf-3 | 192.168.0.77/24 | vEOS-lab | Provisioned | - |
| POD3_LEAFS | l3leaf | pod3-leaf-4 | 192.168.0.78/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod3-spine-1 | 192.168.0.205/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod3-spine-2 | 192.168.0.206/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-1 | 192.168.0.79/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-2 | 192.168.0.80/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-3 | 192.168.0.81/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-4 | 192.168.0.82/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-5 | 192.168.0.83/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-6 | 192.168.0.84/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-7 | 192.168.0.85/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-8 | 192.168.0.86/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-9 | 192.168.0.87/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-10 | 192.168.0.88/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-11 | 192.168.0.89/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-12 | 192.168.0.90/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-13 | 192.168.0.91/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-14 | 192.168.0.92/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-15 | 192.168.0.93/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-16 | 192.168.0.94/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-17 | 192.168.0.95/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-18 | 192.168.0.96/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-19 | 192.168.0.97/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-20 | 192.168.0.98/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-21 | 192.168.0.99/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-22 | 192.168.0.100/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-23 | 192.168.0.101/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-24 | 192.168.0.102/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-25 | 192.168.0.103/24 | vEOS-lab | Provisioned | - |
| POD4_LEAFS | l3leaf | pod4-leaf-26 | 192.168.0.104/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod4-spine-1 | 192.168.0.207/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | pod4-spine-2 | 192.168.0.208/24 | vEOS-lab | Provisioned | - |
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
| l3leaf | pod1-leaf-5 | Ethernet1 | spine | pod1-spine-1 | Ethernet7 |
| l3leaf | pod1-leaf-5 | Ethernet2 | spine | pod1-spine-2 | Ethernet7 |
| l3leaf | pod1-leaf-5 | Ethernet49 | mlag_peer | pod1-leaf-6 | Ethernet49 |
| l3leaf | pod1-leaf-5 | Ethernet50 | mlag_peer | pod1-leaf-6 | Ethernet50 |
| l3leaf | pod1-leaf-6 | Ethernet1 | spine | pod1-spine-1 | Ethernet8 |
| l3leaf | pod1-leaf-6 | Ethernet2 | spine | pod1-spine-2 | Ethernet8 |
| l3leaf | pod1-leaf-7 | Ethernet1 | spine | pod1-spine-1 | Ethernet9 |
| l3leaf | pod1-leaf-7 | Ethernet2 | spine | pod1-spine-2 | Ethernet9 |
| l3leaf | pod1-leaf-7 | Ethernet49 | mlag_peer | pod1-leaf-8 | Ethernet49 |
| l3leaf | pod1-leaf-7 | Ethernet50 | mlag_peer | pod1-leaf-8 | Ethernet50 |
| l3leaf | pod1-leaf-8 | Ethernet1 | spine | pod1-spine-1 | Ethernet10 |
| l3leaf | pod1-leaf-8 | Ethernet2 | spine | pod1-spine-2 | Ethernet10 |
| l3leaf | pod1-leaf-9 | Ethernet1 | spine | pod1-spine-1 | Ethernet11 |
| l3leaf | pod1-leaf-9 | Ethernet2 | spine | pod1-spine-2 | Ethernet11 |
| l3leaf | pod1-leaf-9 | Ethernet49 | mlag_peer | pod1-leaf-10 | Ethernet49 |
| l3leaf | pod1-leaf-9 | Ethernet50 | mlag_peer | pod1-leaf-10 | Ethernet50 |
| l3leaf | pod1-leaf-10 | Ethernet1 | spine | pod1-spine-1 | Ethernet12 |
| l3leaf | pod1-leaf-10 | Ethernet2 | spine | pod1-spine-2 | Ethernet12 |
| l3leaf | pod1-leaf-11 | Ethernet1 | spine | pod1-spine-1 | Ethernet13 |
| l3leaf | pod1-leaf-11 | Ethernet2 | spine | pod1-spine-2 | Ethernet13 |
| l3leaf | pod1-leaf-11 | Ethernet49 | mlag_peer | pod1-leaf-12 | Ethernet49 |
| l3leaf | pod1-leaf-11 | Ethernet50 | mlag_peer | pod1-leaf-12 | Ethernet50 |
| l3leaf | pod1-leaf-12 | Ethernet1 | spine | pod1-spine-1 | Ethernet14 |
| l3leaf | pod1-leaf-12 | Ethernet2 | spine | pod1-spine-2 | Ethernet14 |
| l3leaf | pod1-leaf-13 | Ethernet1 | spine | pod1-spine-1 | Ethernet15 |
| l3leaf | pod1-leaf-13 | Ethernet2 | spine | pod1-spine-2 | Ethernet15 |
| l3leaf | pod1-leaf-13 | Ethernet49 | mlag_peer | pod1-leaf-14 | Ethernet49 |
| l3leaf | pod1-leaf-13 | Ethernet50 | mlag_peer | pod1-leaf-14 | Ethernet50 |
| l3leaf | pod1-leaf-14 | Ethernet1 | spine | pod1-spine-1 | Ethernet16 |
| l3leaf | pod1-leaf-14 | Ethernet2 | spine | pod1-spine-2 | Ethernet16 |
| l3leaf | pod1-leaf-15 | Ethernet1 | spine | pod1-spine-1 | Ethernet17 |
| l3leaf | pod1-leaf-15 | Ethernet2 | spine | pod1-spine-2 | Ethernet17 |
| l3leaf | pod1-leaf-15 | Ethernet49 | mlag_peer | pod1-leaf-16 | Ethernet49 |
| l3leaf | pod1-leaf-15 | Ethernet50 | mlag_peer | pod1-leaf-16 | Ethernet50 |
| l3leaf | pod1-leaf-16 | Ethernet1 | spine | pod1-spine-1 | Ethernet18 |
| l3leaf | pod1-leaf-16 | Ethernet2 | spine | pod1-spine-2 | Ethernet18 |
| spine | pod1-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet1 |
| spine | pod1-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet1 |
| spine | pod1-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet2 |
| spine | pod1-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet2 |
| l3leaf | pod2-leaf-1 | Ethernet1 | spine | pod2-spine-1 | Ethernet3 |
| l3leaf | pod2-leaf-1 | Ethernet2 | spine | pod2-spine-2 | Ethernet3 |
| l3leaf | pod2-leaf-1 | Ethernet49 | mlag_peer | pod2-leaf-2 | Ethernet49 |
| l3leaf | pod2-leaf-1 | Ethernet50 | mlag_peer | pod2-leaf-2 | Ethernet50 |
| l3leaf | pod2-leaf-2 | Ethernet1 | spine | pod2-spine-1 | Ethernet4 |
| l3leaf | pod2-leaf-2 | Ethernet2 | spine | pod2-spine-2 | Ethernet4 |
| l3leaf | pod2-leaf-3 | Ethernet1 | spine | pod2-spine-1 | Ethernet5 |
| l3leaf | pod2-leaf-3 | Ethernet2 | spine | pod2-spine-2 | Ethernet5 |
| l3leaf | pod2-leaf-3 | Ethernet49 | mlag_peer | pod2-leaf-4 | Ethernet49 |
| l3leaf | pod2-leaf-3 | Ethernet50 | mlag_peer | pod2-leaf-4 | Ethernet50 |
| l3leaf | pod2-leaf-4 | Ethernet1 | spine | pod2-spine-1 | Ethernet6 |
| l3leaf | pod2-leaf-4 | Ethernet2 | spine | pod2-spine-2 | Ethernet6 |
| l3leaf | pod2-leaf-5 | Ethernet1 | spine | pod2-spine-1 | Ethernet7 |
| l3leaf | pod2-leaf-5 | Ethernet2 | spine | pod2-spine-2 | Ethernet7 |
| l3leaf | pod2-leaf-5 | Ethernet49 | mlag_peer | pod2-leaf-6 | Ethernet49 |
| l3leaf | pod2-leaf-5 | Ethernet50 | mlag_peer | pod2-leaf-6 | Ethernet50 |
| l3leaf | pod2-leaf-6 | Ethernet1 | spine | pod2-spine-1 | Ethernet8 |
| l3leaf | pod2-leaf-6 | Ethernet2 | spine | pod2-spine-2 | Ethernet8 |
| l3leaf | pod2-leaf-7 | Ethernet1 | spine | pod2-spine-1 | Ethernet9 |
| l3leaf | pod2-leaf-7 | Ethernet2 | spine | pod2-spine-2 | Ethernet9 |
| l3leaf | pod2-leaf-7 | Ethernet49 | mlag_peer | pod2-leaf-8 | Ethernet49 |
| l3leaf | pod2-leaf-7 | Ethernet50 | mlag_peer | pod2-leaf-8 | Ethernet50 |
| l3leaf | pod2-leaf-8 | Ethernet1 | spine | pod2-spine-1 | Ethernet10 |
| l3leaf | pod2-leaf-8 | Ethernet2 | spine | pod2-spine-2 | Ethernet10 |
| l3leaf | pod2-leaf-9 | Ethernet1 | spine | pod2-spine-1 | Ethernet11 |
| l3leaf | pod2-leaf-9 | Ethernet2 | spine | pod2-spine-2 | Ethernet11 |
| l3leaf | pod2-leaf-9 | Ethernet49 | mlag_peer | pod2-leaf-10 | Ethernet49 |
| l3leaf | pod2-leaf-9 | Ethernet50 | mlag_peer | pod2-leaf-10 | Ethernet50 |
| l3leaf | pod2-leaf-10 | Ethernet1 | spine | pod2-spine-1 | Ethernet12 |
| l3leaf | pod2-leaf-10 | Ethernet2 | spine | pod2-spine-2 | Ethernet12 |
| l3leaf | pod2-leaf-11 | Ethernet1 | spine | pod2-spine-1 | Ethernet13 |
| l3leaf | pod2-leaf-11 | Ethernet2 | spine | pod2-spine-2 | Ethernet13 |
| l3leaf | pod2-leaf-11 | Ethernet49 | mlag_peer | pod2-leaf-12 | Ethernet49 |
| l3leaf | pod2-leaf-11 | Ethernet50 | mlag_peer | pod2-leaf-12 | Ethernet50 |
| l3leaf | pod2-leaf-12 | Ethernet1 | spine | pod2-spine-1 | Ethernet14 |
| l3leaf | pod2-leaf-12 | Ethernet2 | spine | pod2-spine-2 | Ethernet14 |
| l3leaf | pod2-leaf-13 | Ethernet1 | spine | pod2-spine-1 | Ethernet15 |
| l3leaf | pod2-leaf-13 | Ethernet2 | spine | pod2-spine-2 | Ethernet15 |
| l3leaf | pod2-leaf-13 | Ethernet49 | mlag_peer | pod2-leaf-14 | Ethernet49 |
| l3leaf | pod2-leaf-13 | Ethernet50 | mlag_peer | pod2-leaf-14 | Ethernet50 |
| l3leaf | pod2-leaf-14 | Ethernet1 | spine | pod2-spine-1 | Ethernet16 |
| l3leaf | pod2-leaf-14 | Ethernet2 | spine | pod2-spine-2 | Ethernet16 |
| l3leaf | pod2-leaf-15 | Ethernet1 | spine | pod2-spine-1 | Ethernet17 |
| l3leaf | pod2-leaf-15 | Ethernet2 | spine | pod2-spine-2 | Ethernet17 |
| l3leaf | pod2-leaf-15 | Ethernet49 | mlag_peer | pod2-leaf-16 | Ethernet49 |
| l3leaf | pod2-leaf-15 | Ethernet50 | mlag_peer | pod2-leaf-16 | Ethernet50 |
| l3leaf | pod2-leaf-16 | Ethernet1 | spine | pod2-spine-1 | Ethernet18 |
| l3leaf | pod2-leaf-16 | Ethernet2 | spine | pod2-spine-2 | Ethernet18 |
| spine | pod2-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet3 |
| spine | pod2-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet3 |
| spine | pod2-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet4 |
| spine | pod2-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet4 |
| l3leaf | pod3-leaf-1 | Ethernet1 | spine | pod3-spine-1 | Ethernet3 |
| l3leaf | pod3-leaf-1 | Ethernet2 | spine | pod3-spine-2 | Ethernet3 |
| l3leaf | pod3-leaf-1 | Ethernet49 | mlag_peer | pod3-leaf-2 | Ethernet49 |
| l3leaf | pod3-leaf-1 | Ethernet50 | mlag_peer | pod3-leaf-2 | Ethernet50 |
| l3leaf | pod3-leaf-2 | Ethernet1 | spine | pod3-spine-1 | Ethernet4 |
| l3leaf | pod3-leaf-2 | Ethernet2 | spine | pod3-spine-2 | Ethernet4 |
| l3leaf | pod3-leaf-3 | Ethernet1 | spine | pod3-spine-1 | Ethernet5 |
| l3leaf | pod3-leaf-3 | Ethernet2 | spine | pod3-spine-2 | Ethernet5 |
| l3leaf | pod3-leaf-3 | Ethernet49 | mlag_peer | pod3-leaf-4 | Ethernet49 |
| l3leaf | pod3-leaf-3 | Ethernet50 | mlag_peer | pod3-leaf-4 | Ethernet50 |
| l3leaf | pod3-leaf-4 | Ethernet1 | spine | pod3-spine-1 | Ethernet6 |
| l3leaf | pod3-leaf-4 | Ethernet2 | spine | pod3-spine-2 | Ethernet6 |
| spine | pod3-spine-1 | Ethernet1 | super-spine | super-spine-1 | Ethernet5 |
| spine | pod3-spine-1 | Ethernet2 | super-spine | super-spine-2 | Ethernet5 |
| spine | pod3-spine-2 | Ethernet1 | super-spine | super-spine-1 | Ethernet6 |
| spine | pod3-spine-2 | Ethernet2 | super-spine | super-spine-2 | Ethernet6 |
| l3leaf | pod4-leaf-1 | Ethernet1 | spine | pod4-spine-1 | Ethernet3 |
| l3leaf | pod4-leaf-1 | Ethernet2 | spine | pod4-spine-2 | Ethernet3 |
| l3leaf | pod4-leaf-1 | Ethernet49 | mlag_peer | pod4-leaf-2 | Ethernet49 |
| l3leaf | pod4-leaf-1 | Ethernet50 | mlag_peer | pod4-leaf-2 | Ethernet50 |
| l3leaf | pod4-leaf-2 | Ethernet1 | spine | pod4-spine-1 | Ethernet4 |
| l3leaf | pod4-leaf-2 | Ethernet2 | spine | pod4-spine-2 | Ethernet4 |
| l3leaf | pod4-leaf-3 | Ethernet1 | spine | pod4-spine-1 | Ethernet5 |
| l3leaf | pod4-leaf-3 | Ethernet2 | spine | pod4-spine-2 | Ethernet5 |
| l3leaf | pod4-leaf-3 | Ethernet49 | mlag_peer | pod4-leaf-4 | Ethernet49 |
| l3leaf | pod4-leaf-3 | Ethernet50 | mlag_peer | pod4-leaf-4 | Ethernet50 |
| l3leaf | pod4-leaf-4 | Ethernet1 | spine | pod4-spine-1 | Ethernet6 |
| l3leaf | pod4-leaf-4 | Ethernet2 | spine | pod4-spine-2 | Ethernet6 |
| l3leaf | pod4-leaf-5 | Ethernet1 | spine | pod4-spine-1 | Ethernet7 |
| l3leaf | pod4-leaf-5 | Ethernet2 | spine | pod4-spine-2 | Ethernet7 |
| l3leaf | pod4-leaf-5 | Ethernet49 | mlag_peer | pod4-leaf-6 | Ethernet49 |
| l3leaf | pod4-leaf-5 | Ethernet50 | mlag_peer | pod4-leaf-6 | Ethernet50 |
| l3leaf | pod4-leaf-6 | Ethernet1 | spine | pod4-spine-1 | Ethernet8 |
| l3leaf | pod4-leaf-6 | Ethernet2 | spine | pod4-spine-2 | Ethernet8 |
| l3leaf | pod4-leaf-7 | Ethernet1 | spine | pod4-spine-1 | Ethernet9 |
| l3leaf | pod4-leaf-7 | Ethernet2 | spine | pod4-spine-2 | Ethernet9 |
| l3leaf | pod4-leaf-7 | Ethernet49 | mlag_peer | pod4-leaf-8 | Ethernet49 |
| l3leaf | pod4-leaf-7 | Ethernet50 | mlag_peer | pod4-leaf-8 | Ethernet50 |
| l3leaf | pod4-leaf-8 | Ethernet1 | spine | pod4-spine-1 | Ethernet10 |
| l3leaf | pod4-leaf-8 | Ethernet2 | spine | pod4-spine-2 | Ethernet10 |
| l3leaf | pod4-leaf-9 | Ethernet1 | spine | pod4-spine-1 | Ethernet11 |
| l3leaf | pod4-leaf-9 | Ethernet2 | spine | pod4-spine-2 | Ethernet11 |
| l3leaf | pod4-leaf-9 | Ethernet49 | mlag_peer | pod4-leaf-10 | Ethernet49 |
| l3leaf | pod4-leaf-9 | Ethernet50 | mlag_peer | pod4-leaf-10 | Ethernet50 |
| l3leaf | pod4-leaf-10 | Ethernet1 | spine | pod4-spine-1 | Ethernet12 |
| l3leaf | pod4-leaf-10 | Ethernet2 | spine | pod4-spine-2 | Ethernet12 |
| l3leaf | pod4-leaf-11 | Ethernet1 | spine | pod4-spine-1 | Ethernet13 |
| l3leaf | pod4-leaf-11 | Ethernet2 | spine | pod4-spine-2 | Ethernet13 |
| l3leaf | pod4-leaf-11 | Ethernet49 | mlag_peer | pod4-leaf-12 | Ethernet49 |
| l3leaf | pod4-leaf-11 | Ethernet50 | mlag_peer | pod4-leaf-12 | Ethernet50 |
| l3leaf | pod4-leaf-12 | Ethernet1 | spine | pod4-spine-1 | Ethernet14 |
| l3leaf | pod4-leaf-12 | Ethernet2 | spine | pod4-spine-2 | Ethernet14 |
| l3leaf | pod4-leaf-13 | Ethernet1 | spine | pod4-spine-1 | Ethernet15 |
| l3leaf | pod4-leaf-13 | Ethernet2 | spine | pod4-spine-2 | Ethernet15 |
| l3leaf | pod4-leaf-13 | Ethernet49 | mlag_peer | pod4-leaf-14 | Ethernet49 |
| l3leaf | pod4-leaf-13 | Ethernet50 | mlag_peer | pod4-leaf-14 | Ethernet50 |
| l3leaf | pod4-leaf-14 | Ethernet1 | spine | pod4-spine-1 | Ethernet16 |
| l3leaf | pod4-leaf-14 | Ethernet2 | spine | pod4-spine-2 | Ethernet16 |
| l3leaf | pod4-leaf-15 | Ethernet1 | spine | pod4-spine-1 | Ethernet17 |
| l3leaf | pod4-leaf-15 | Ethernet2 | spine | pod4-spine-2 | Ethernet17 |
| l3leaf | pod4-leaf-15 | Ethernet49 | mlag_peer | pod4-leaf-16 | Ethernet49 |
| l3leaf | pod4-leaf-15 | Ethernet50 | mlag_peer | pod4-leaf-16 | Ethernet50 |
| l3leaf | pod4-leaf-16 | Ethernet1 | spine | pod4-spine-1 | Ethernet18 |
| l3leaf | pod4-leaf-16 | Ethernet2 | spine | pod4-spine-2 | Ethernet18 |
| l3leaf | pod4-leaf-17 | Ethernet1 | spine | pod4-spine-1 | Ethernet19 |
| l3leaf | pod4-leaf-17 | Ethernet2 | spine | pod4-spine-2 | Ethernet19 |
| l3leaf | pod4-leaf-17 | Ethernet49 | mlag_peer | pod4-leaf-18 | Ethernet49 |
| l3leaf | pod4-leaf-17 | Ethernet50 | mlag_peer | pod4-leaf-18 | Ethernet50 |
| l3leaf | pod4-leaf-18 | Ethernet1 | spine | pod4-spine-1 | Ethernet20 |
| l3leaf | pod4-leaf-18 | Ethernet2 | spine | pod4-spine-2 | Ethernet20 |
| l3leaf | pod4-leaf-19 | Ethernet1 | spine | pod4-spine-1 | Ethernet21 |
| l3leaf | pod4-leaf-19 | Ethernet2 | spine | pod4-spine-2 | Ethernet21 |
| l3leaf | pod4-leaf-19 | Ethernet49 | mlag_peer | pod4-leaf-20 | Ethernet49 |
| l3leaf | pod4-leaf-19 | Ethernet50 | mlag_peer | pod4-leaf-20 | Ethernet50 |
| l3leaf | pod4-leaf-20 | Ethernet1 | spine | pod4-spine-1 | Ethernet22 |
| l3leaf | pod4-leaf-20 | Ethernet2 | spine | pod4-spine-2 | Ethernet22 |
| l3leaf | pod4-leaf-21 | Ethernet1 | spine | pod4-spine-1 | Ethernet23 |
| l3leaf | pod4-leaf-21 | Ethernet2 | spine | pod4-spine-2 | Ethernet23 |
| l3leaf | pod4-leaf-21 | Ethernet49 | mlag_peer | pod4-leaf-22 | Ethernet49 |
| l3leaf | pod4-leaf-21 | Ethernet50 | mlag_peer | pod4-leaf-22 | Ethernet50 |
| l3leaf | pod4-leaf-22 | Ethernet1 | spine | pod4-spine-1 | Ethernet24 |
| l3leaf | pod4-leaf-22 | Ethernet2 | spine | pod4-spine-2 | Ethernet24 |
| l3leaf | pod4-leaf-23 | Ethernet1 | spine | pod4-spine-1 | Ethernet25 |
| l3leaf | pod4-leaf-23 | Ethernet2 | spine | pod4-spine-2 | Ethernet25 |
| l3leaf | pod4-leaf-23 | Ethernet49 | mlag_peer | pod4-leaf-24 | Ethernet49 |
| l3leaf | pod4-leaf-23 | Ethernet50 | mlag_peer | pod4-leaf-24 | Ethernet50 |
| l3leaf | pod4-leaf-24 | Ethernet1 | spine | pod4-spine-1 | Ethernet26 |
| l3leaf | pod4-leaf-24 | Ethernet2 | spine | pod4-spine-2 | Ethernet26 |
| l3leaf | pod4-leaf-25 | Ethernet1 | spine | pod4-spine-1 | Ethernet27 |
| l3leaf | pod4-leaf-25 | Ethernet2 | spine | pod4-spine-2 | Ethernet27 |
| l3leaf | pod4-leaf-25 | Ethernet49 | mlag_peer | pod4-leaf-26 | Ethernet49 |
| l3leaf | pod4-leaf-25 | Ethernet50 | mlag_peer | pod4-leaf-26 | Ethernet50 |
| l3leaf | pod4-leaf-26 | Ethernet1 | spine | pod4-spine-1 | Ethernet28 |
| l3leaf | pod4-leaf-26 | Ethernet2 | spine | pod4-spine-2 | Ethernet28 |
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
| 10.255.252.0/24 | 256 | 104 | 40.63 % |
| 10.255.253.0/24 | 256 | 16 | 6.25 % |
| 10.255.254.0/24 | 256 | 64 | 25.0 % |
| 10.255.255.0/24 | 256 | 64 | 25.0 % |

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
| pod1-leaf-5 | Ethernet1 | 10.255.255.17/31 | pod1-spine-1 | Ethernet7 | 10.255.255.16/31 |
| pod1-leaf-5 | Ethernet2 | 10.255.255.19/31 | pod1-spine-2 | Ethernet7 | 10.255.255.18/31 |
| pod1-leaf-6 | Ethernet1 | 10.255.255.21/31 | pod1-spine-1 | Ethernet8 | 10.255.255.20/31 |
| pod1-leaf-6 | Ethernet2 | 10.255.255.23/31 | pod1-spine-2 | Ethernet8 | 10.255.255.22/31 |
| pod1-leaf-7 | Ethernet1 | 10.255.255.25/31 | pod1-spine-1 | Ethernet9 | 10.255.255.24/31 |
| pod1-leaf-7 | Ethernet2 | 10.255.255.27/31 | pod1-spine-2 | Ethernet9 | 10.255.255.26/31 |
| pod1-leaf-8 | Ethernet1 | 10.255.255.29/31 | pod1-spine-1 | Ethernet10 | 10.255.255.28/31 |
| pod1-leaf-8 | Ethernet2 | 10.255.255.31/31 | pod1-spine-2 | Ethernet10 | 10.255.255.30/31 |
| pod1-leaf-9 | Ethernet1 | 10.255.255.33/31 | pod1-spine-1 | Ethernet11 | 10.255.255.32/31 |
| pod1-leaf-9 | Ethernet2 | 10.255.255.35/31 | pod1-spine-2 | Ethernet11 | 10.255.255.34/31 |
| pod1-leaf-10 | Ethernet1 | 10.255.255.37/31 | pod1-spine-1 | Ethernet12 | 10.255.255.36/31 |
| pod1-leaf-10 | Ethernet2 | 10.255.255.39/31 | pod1-spine-2 | Ethernet12 | 10.255.255.38/31 |
| pod1-leaf-11 | Ethernet1 | 10.255.255.41/31 | pod1-spine-1 | Ethernet13 | 10.255.255.40/31 |
| pod1-leaf-11 | Ethernet2 | 10.255.255.43/31 | pod1-spine-2 | Ethernet13 | 10.255.255.42/31 |
| pod1-leaf-12 | Ethernet1 | 10.255.255.45/31 | pod1-spine-1 | Ethernet14 | 10.255.255.44/31 |
| pod1-leaf-12 | Ethernet2 | 10.255.255.47/31 | pod1-spine-2 | Ethernet14 | 10.255.255.46/31 |
| pod1-leaf-13 | Ethernet1 | 10.255.255.49/31 | pod1-spine-1 | Ethernet15 | 10.255.255.48/31 |
| pod1-leaf-13 | Ethernet2 | 10.255.255.51/31 | pod1-spine-2 | Ethernet15 | 10.255.255.50/31 |
| pod1-leaf-14 | Ethernet1 | 10.255.255.53/31 | pod1-spine-1 | Ethernet16 | 10.255.255.52/31 |
| pod1-leaf-14 | Ethernet2 | 10.255.255.55/31 | pod1-spine-2 | Ethernet16 | 10.255.255.54/31 |
| pod1-leaf-15 | Ethernet1 | 10.255.255.57/31 | pod1-spine-1 | Ethernet17 | 10.255.255.56/31 |
| pod1-leaf-15 | Ethernet2 | 10.255.255.59/31 | pod1-spine-2 | Ethernet17 | 10.255.255.58/31 |
| pod1-leaf-16 | Ethernet1 | 10.255.255.61/31 | pod1-spine-1 | Ethernet18 | 10.255.255.60/31 |
| pod1-leaf-16 | Ethernet2 | 10.255.255.63/31 | pod1-spine-2 | Ethernet18 | 10.255.255.62/31 |
| pod1-spine-1 | Ethernet1 | 10.255.250.1/31 | super-spine-1 | Ethernet1 | 10.255.250.0/31 |
| pod1-spine-1 | Ethernet2 | 10.255.250.3/31 | super-spine-2 | Ethernet1 | 10.255.250.2/31 |
| pod1-spine-2 | Ethernet1 | 10.255.250.5/31 | super-spine-1 | Ethernet2 | 10.255.250.4/31 |
| pod1-spine-2 | Ethernet2 | 10.255.250.7/31 | super-spine-2 | Ethernet2 | 10.255.250.6/31 |
| pod2-leaf-1 | Ethernet1 | 10.255.254.1/31 | pod2-spine-1 | Ethernet3 | 10.255.254.0/31 |
| pod2-leaf-1 | Ethernet2 | 10.255.254.3/31 | pod2-spine-2 | Ethernet3 | 10.255.254.2/31 |
| pod2-leaf-2 | Ethernet1 | 10.255.254.5/31 | pod2-spine-1 | Ethernet4 | 10.255.254.4/31 |
| pod2-leaf-2 | Ethernet2 | 10.255.254.7/31 | pod2-spine-2 | Ethernet4 | 10.255.254.6/31 |
| pod2-leaf-3 | Ethernet1 | 10.255.254.9/31 | pod2-spine-1 | Ethernet5 | 10.255.254.8/31 |
| pod2-leaf-3 | Ethernet2 | 10.255.254.11/31 | pod2-spine-2 | Ethernet5 | 10.255.254.10/31 |
| pod2-leaf-4 | Ethernet1 | 10.255.254.13/31 | pod2-spine-1 | Ethernet6 | 10.255.254.12/31 |
| pod2-leaf-4 | Ethernet2 | 10.255.254.15/31 | pod2-spine-2 | Ethernet6 | 10.255.254.14/31 |
| pod2-leaf-5 | Ethernet1 | 10.255.254.17/31 | pod2-spine-1 | Ethernet7 | 10.255.254.16/31 |
| pod2-leaf-5 | Ethernet2 | 10.255.254.19/31 | pod2-spine-2 | Ethernet7 | 10.255.254.18/31 |
| pod2-leaf-6 | Ethernet1 | 10.255.254.21/31 | pod2-spine-1 | Ethernet8 | 10.255.254.20/31 |
| pod2-leaf-6 | Ethernet2 | 10.255.254.23/31 | pod2-spine-2 | Ethernet8 | 10.255.254.22/31 |
| pod2-leaf-7 | Ethernet1 | 10.255.254.25/31 | pod2-spine-1 | Ethernet9 | 10.255.254.24/31 |
| pod2-leaf-7 | Ethernet2 | 10.255.254.27/31 | pod2-spine-2 | Ethernet9 | 10.255.254.26/31 |
| pod2-leaf-8 | Ethernet1 | 10.255.254.29/31 | pod2-spine-1 | Ethernet10 | 10.255.254.28/31 |
| pod2-leaf-8 | Ethernet2 | 10.255.254.31/31 | pod2-spine-2 | Ethernet10 | 10.255.254.30/31 |
| pod2-leaf-9 | Ethernet1 | 10.255.254.33/31 | pod2-spine-1 | Ethernet11 | 10.255.254.32/31 |
| pod2-leaf-9 | Ethernet2 | 10.255.254.35/31 | pod2-spine-2 | Ethernet11 | 10.255.254.34/31 |
| pod2-leaf-10 | Ethernet1 | 10.255.254.37/31 | pod2-spine-1 | Ethernet12 | 10.255.254.36/31 |
| pod2-leaf-10 | Ethernet2 | 10.255.254.39/31 | pod2-spine-2 | Ethernet12 | 10.255.254.38/31 |
| pod2-leaf-11 | Ethernet1 | 10.255.254.41/31 | pod2-spine-1 | Ethernet13 | 10.255.254.40/31 |
| pod2-leaf-11 | Ethernet2 | 10.255.254.43/31 | pod2-spine-2 | Ethernet13 | 10.255.254.42/31 |
| pod2-leaf-12 | Ethernet1 | 10.255.254.45/31 | pod2-spine-1 | Ethernet14 | 10.255.254.44/31 |
| pod2-leaf-12 | Ethernet2 | 10.255.254.47/31 | pod2-spine-2 | Ethernet14 | 10.255.254.46/31 |
| pod2-leaf-13 | Ethernet1 | 10.255.254.49/31 | pod2-spine-1 | Ethernet15 | 10.255.254.48/31 |
| pod2-leaf-13 | Ethernet2 | 10.255.254.51/31 | pod2-spine-2 | Ethernet15 | 10.255.254.50/31 |
| pod2-leaf-14 | Ethernet1 | 10.255.254.53/31 | pod2-spine-1 | Ethernet16 | 10.255.254.52/31 |
| pod2-leaf-14 | Ethernet2 | 10.255.254.55/31 | pod2-spine-2 | Ethernet16 | 10.255.254.54/31 |
| pod2-leaf-15 | Ethernet1 | 10.255.254.57/31 | pod2-spine-1 | Ethernet17 | 10.255.254.56/31 |
| pod2-leaf-15 | Ethernet2 | 10.255.254.59/31 | pod2-spine-2 | Ethernet17 | 10.255.254.58/31 |
| pod2-leaf-16 | Ethernet1 | 10.255.254.61/31 | pod2-spine-1 | Ethernet18 | 10.255.254.60/31 |
| pod2-leaf-16 | Ethernet2 | 10.255.254.63/31 | pod2-spine-2 | Ethernet18 | 10.255.254.62/31 |
| pod2-spine-1 | Ethernet1 | 10.255.250.9/31 | super-spine-1 | Ethernet3 | 10.255.250.8/31 |
| pod2-spine-1 | Ethernet2 | 10.255.250.11/31 | super-spine-2 | Ethernet3 | 10.255.250.10/31 |
| pod2-spine-2 | Ethernet1 | 10.255.250.13/31 | super-spine-1 | Ethernet4 | 10.255.250.12/31 |
| pod2-spine-2 | Ethernet2 | 10.255.250.15/31 | super-spine-2 | Ethernet4 | 10.255.250.14/31 |
| pod3-leaf-1 | Ethernet1 | 10.255.253.1/31 | pod3-spine-1 | Ethernet3 | 10.255.253.0/31 |
| pod3-leaf-1 | Ethernet2 | 10.255.253.3/31 | pod3-spine-2 | Ethernet3 | 10.255.253.2/31 |
| pod3-leaf-2 | Ethernet1 | 10.255.253.5/31 | pod3-spine-1 | Ethernet4 | 10.255.253.4/31 |
| pod3-leaf-2 | Ethernet2 | 10.255.253.7/31 | pod3-spine-2 | Ethernet4 | 10.255.253.6/31 |
| pod3-leaf-3 | Ethernet1 | 10.255.253.9/31 | pod3-spine-1 | Ethernet5 | 10.255.253.8/31 |
| pod3-leaf-3 | Ethernet2 | 10.255.253.11/31 | pod3-spine-2 | Ethernet5 | 10.255.253.10/31 |
| pod3-leaf-4 | Ethernet1 | 10.255.253.13/31 | pod3-spine-1 | Ethernet6 | 10.255.253.12/31 |
| pod3-leaf-4 | Ethernet2 | 10.255.253.15/31 | pod3-spine-2 | Ethernet6 | 10.255.253.14/31 |
| pod3-spine-1 | Ethernet1 | 10.255.250.17/31 | super-spine-1 | Ethernet5 | 10.255.250.16/31 |
| pod3-spine-1 | Ethernet2 | 10.255.250.19/31 | super-spine-2 | Ethernet5 | 10.255.250.18/31 |
| pod3-spine-2 | Ethernet1 | 10.255.250.21/31 | super-spine-1 | Ethernet6 | 10.255.250.20/31 |
| pod3-spine-2 | Ethernet2 | 10.255.250.23/31 | super-spine-2 | Ethernet6 | 10.255.250.22/31 |
| pod4-leaf-1 | Ethernet1 | 10.255.252.1/31 | pod4-spine-1 | Ethernet3 | 10.255.252.0/31 |
| pod4-leaf-1 | Ethernet2 | 10.255.252.3/31 | pod4-spine-2 | Ethernet3 | 10.255.252.2/31 |
| pod4-leaf-2 | Ethernet1 | 10.255.252.5/31 | pod4-spine-1 | Ethernet4 | 10.255.252.4/31 |
| pod4-leaf-2 | Ethernet2 | 10.255.252.7/31 | pod4-spine-2 | Ethernet4 | 10.255.252.6/31 |
| pod4-leaf-3 | Ethernet1 | 10.255.252.9/31 | pod4-spine-1 | Ethernet5 | 10.255.252.8/31 |
| pod4-leaf-3 | Ethernet2 | 10.255.252.11/31 | pod4-spine-2 | Ethernet5 | 10.255.252.10/31 |
| pod4-leaf-4 | Ethernet1 | 10.255.252.13/31 | pod4-spine-1 | Ethernet6 | 10.255.252.12/31 |
| pod4-leaf-4 | Ethernet2 | 10.255.252.15/31 | pod4-spine-2 | Ethernet6 | 10.255.252.14/31 |
| pod4-leaf-5 | Ethernet1 | 10.255.252.17/31 | pod4-spine-1 | Ethernet7 | 10.255.252.16/31 |
| pod4-leaf-5 | Ethernet2 | 10.255.252.19/31 | pod4-spine-2 | Ethernet7 | 10.255.252.18/31 |
| pod4-leaf-6 | Ethernet1 | 10.255.252.21/31 | pod4-spine-1 | Ethernet8 | 10.255.252.20/31 |
| pod4-leaf-6 | Ethernet2 | 10.255.252.23/31 | pod4-spine-2 | Ethernet8 | 10.255.252.22/31 |
| pod4-leaf-7 | Ethernet1 | 10.255.252.25/31 | pod4-spine-1 | Ethernet9 | 10.255.252.24/31 |
| pod4-leaf-7 | Ethernet2 | 10.255.252.27/31 | pod4-spine-2 | Ethernet9 | 10.255.252.26/31 |
| pod4-leaf-8 | Ethernet1 | 10.255.252.29/31 | pod4-spine-1 | Ethernet10 | 10.255.252.28/31 |
| pod4-leaf-8 | Ethernet2 | 10.255.252.31/31 | pod4-spine-2 | Ethernet10 | 10.255.252.30/31 |
| pod4-leaf-9 | Ethernet1 | 10.255.252.33/31 | pod4-spine-1 | Ethernet11 | 10.255.252.32/31 |
| pod4-leaf-9 | Ethernet2 | 10.255.252.35/31 | pod4-spine-2 | Ethernet11 | 10.255.252.34/31 |
| pod4-leaf-10 | Ethernet1 | 10.255.252.37/31 | pod4-spine-1 | Ethernet12 | 10.255.252.36/31 |
| pod4-leaf-10 | Ethernet2 | 10.255.252.39/31 | pod4-spine-2 | Ethernet12 | 10.255.252.38/31 |
| pod4-leaf-11 | Ethernet1 | 10.255.252.41/31 | pod4-spine-1 | Ethernet13 | 10.255.252.40/31 |
| pod4-leaf-11 | Ethernet2 | 10.255.252.43/31 | pod4-spine-2 | Ethernet13 | 10.255.252.42/31 |
| pod4-leaf-12 | Ethernet1 | 10.255.252.45/31 | pod4-spine-1 | Ethernet14 | 10.255.252.44/31 |
| pod4-leaf-12 | Ethernet2 | 10.255.252.47/31 | pod4-spine-2 | Ethernet14 | 10.255.252.46/31 |
| pod4-leaf-13 | Ethernet1 | 10.255.252.49/31 | pod4-spine-1 | Ethernet15 | 10.255.252.48/31 |
| pod4-leaf-13 | Ethernet2 | 10.255.252.51/31 | pod4-spine-2 | Ethernet15 | 10.255.252.50/31 |
| pod4-leaf-14 | Ethernet1 | 10.255.252.53/31 | pod4-spine-1 | Ethernet16 | 10.255.252.52/31 |
| pod4-leaf-14 | Ethernet2 | 10.255.252.55/31 | pod4-spine-2 | Ethernet16 | 10.255.252.54/31 |
| pod4-leaf-15 | Ethernet1 | 10.255.252.57/31 | pod4-spine-1 | Ethernet17 | 10.255.252.56/31 |
| pod4-leaf-15 | Ethernet2 | 10.255.252.59/31 | pod4-spine-2 | Ethernet17 | 10.255.252.58/31 |
| pod4-leaf-16 | Ethernet1 | 10.255.252.61/31 | pod4-spine-1 | Ethernet18 | 10.255.252.60/31 |
| pod4-leaf-16 | Ethernet2 | 10.255.252.63/31 | pod4-spine-2 | Ethernet18 | 10.255.252.62/31 |
| pod4-leaf-17 | Ethernet1 | 10.255.252.65/31 | pod4-spine-1 | Ethernet19 | 10.255.252.64/31 |
| pod4-leaf-17 | Ethernet2 | 10.255.252.67/31 | pod4-spine-2 | Ethernet19 | 10.255.252.66/31 |
| pod4-leaf-18 | Ethernet1 | 10.255.252.69/31 | pod4-spine-1 | Ethernet20 | 10.255.252.68/31 |
| pod4-leaf-18 | Ethernet2 | 10.255.252.71/31 | pod4-spine-2 | Ethernet20 | 10.255.252.70/31 |
| pod4-leaf-19 | Ethernet1 | 10.255.252.73/31 | pod4-spine-1 | Ethernet21 | 10.255.252.72/31 |
| pod4-leaf-19 | Ethernet2 | 10.255.252.75/31 | pod4-spine-2 | Ethernet21 | 10.255.252.74/31 |
| pod4-leaf-20 | Ethernet1 | 10.255.252.77/31 | pod4-spine-1 | Ethernet22 | 10.255.252.76/31 |
| pod4-leaf-20 | Ethernet2 | 10.255.252.79/31 | pod4-spine-2 | Ethernet22 | 10.255.252.78/31 |
| pod4-leaf-21 | Ethernet1 | 10.255.252.81/31 | pod4-spine-1 | Ethernet23 | 10.255.252.80/31 |
| pod4-leaf-21 | Ethernet2 | 10.255.252.83/31 | pod4-spine-2 | Ethernet23 | 10.255.252.82/31 |
| pod4-leaf-22 | Ethernet1 | 10.255.252.85/31 | pod4-spine-1 | Ethernet24 | 10.255.252.84/31 |
| pod4-leaf-22 | Ethernet2 | 10.255.252.87/31 | pod4-spine-2 | Ethernet24 | 10.255.252.86/31 |
| pod4-leaf-23 | Ethernet1 | 10.255.252.89/31 | pod4-spine-1 | Ethernet25 | 10.255.252.88/31 |
| pod4-leaf-23 | Ethernet2 | 10.255.252.91/31 | pod4-spine-2 | Ethernet25 | 10.255.252.90/31 |
| pod4-leaf-24 | Ethernet1 | 10.255.252.93/31 | pod4-spine-1 | Ethernet26 | 10.255.252.92/31 |
| pod4-leaf-24 | Ethernet2 | 10.255.252.95/31 | pod4-spine-2 | Ethernet26 | 10.255.252.94/31 |
| pod4-leaf-25 | Ethernet1 | 10.255.252.97/31 | pod4-spine-1 | Ethernet27 | 10.255.252.96/31 |
| pod4-leaf-25 | Ethernet2 | 10.255.252.99/31 | pod4-spine-2 | Ethernet27 | 10.255.252.98/31 |
| pod4-leaf-26 | Ethernet1 | 10.255.252.101/31 | pod4-spine-1 | Ethernet28 | 10.255.252.100/31 |
| pod4-leaf-26 | Ethernet2 | 10.255.252.103/31 | pod4-spine-2 | Ethernet28 | 10.255.252.102/31 |
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
| 100.100.1.0/24 | 256 | 16 | 6.25 % |
| 100.100.2.0/24 | 256 | 16 | 6.25 % |
| 100.100.3.0/24 | 256 | 4 | 1.57 % |
| 100.100.4.0/24 | 256 | 26 | 10.16 % |
| 100.100.5.0/24 | 256 | 2 | 0.79 % |
| 100.100.6.0/26 | 64 | 2 | 3.13 % |
| 100.100.7.0/26 | 64 | 8 | 12.5 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| POD1_LEAFS | pod1-leaf-1 | 100.100.1.1/32 |
| POD1_LEAFS | pod1-leaf-2 | 100.100.1.2/32 |
| POD1_LEAFS | pod1-leaf-3 | 100.100.1.3/32 |
| POD1_LEAFS | pod1-leaf-4 | 100.100.1.4/32 |
| POD1_LEAFS | pod1-leaf-5 | 100.100.1.5/32 |
| POD1_LEAFS | pod1-leaf-6 | 100.100.1.6/32 |
| POD1_LEAFS | pod1-leaf-7 | 100.100.1.7/32 |
| POD1_LEAFS | pod1-leaf-8 | 100.100.1.8/32 |
| POD1_LEAFS | pod1-leaf-9 | 100.100.1.9/32 |
| POD1_LEAFS | pod1-leaf-10 | 100.100.1.10/32 |
| POD1_LEAFS | pod1-leaf-11 | 100.100.1.11/32 |
| POD1_LEAFS | pod1-leaf-12 | 100.100.1.12/32 |
| POD1_LEAFS | pod1-leaf-13 | 100.100.1.13/32 |
| POD1_LEAFS | pod1-leaf-14 | 100.100.1.14/32 |
| POD1_LEAFS | pod1-leaf-15 | 100.100.1.15/32 |
| POD1_LEAFS | pod1-leaf-16 | 100.100.1.16/32 |
| FABRIC | pod1-spine-1 | 100.100.7.1/32 |
| FABRIC | pod1-spine-2 | 100.100.7.2/32 |
| POD2_LEAFS | pod2-leaf-1 | 100.100.2.1/32 |
| POD2_LEAFS | pod2-leaf-2 | 100.100.2.2/32 |
| POD2_LEAFS | pod2-leaf-3 | 100.100.2.3/32 |
| POD2_LEAFS | pod2-leaf-4 | 100.100.2.4/32 |
| POD2_LEAFS | pod2-leaf-5 | 100.100.2.5/32 |
| POD2_LEAFS | pod2-leaf-6 | 100.100.2.6/32 |
| POD2_LEAFS | pod2-leaf-7 | 100.100.2.7/32 |
| POD2_LEAFS | pod2-leaf-8 | 100.100.2.8/32 |
| POD2_LEAFS | pod2-leaf-9 | 100.100.2.9/32 |
| POD2_LEAFS | pod2-leaf-10 | 100.100.2.10/32 |
| POD2_LEAFS | pod2-leaf-11 | 100.100.2.11/32 |
| POD2_LEAFS | pod2-leaf-12 | 100.100.2.12/32 |
| POD2_LEAFS | pod2-leaf-13 | 100.100.2.13/32 |
| POD2_LEAFS | pod2-leaf-14 | 100.100.2.14/32 |
| POD2_LEAFS | pod2-leaf-15 | 100.100.2.15/32 |
| POD2_LEAFS | pod2-leaf-16 | 100.100.2.16/32 |
| FABRIC | pod2-spine-1 | 100.100.7.3/32 |
| FABRIC | pod2-spine-2 | 100.100.7.4/32 |
| POD3_LEAFS | pod3-leaf-1 | 100.100.3.1/32 |
| POD3_LEAFS | pod3-leaf-2 | 100.100.3.2/32 |
| POD3_LEAFS | pod3-leaf-3 | 100.100.3.3/32 |
| POD3_LEAFS | pod3-leaf-4 | 100.100.3.4/32 |
| FABRIC | pod3-spine-1 | 100.100.7.5/32 |
| FABRIC | pod3-spine-2 | 100.100.7.6/32 |
| POD4_LEAFS | pod4-leaf-1 | 100.100.4.1/32 |
| POD4_LEAFS | pod4-leaf-2 | 100.100.4.2/32 |
| POD4_LEAFS | pod4-leaf-3 | 100.100.4.3/32 |
| POD4_LEAFS | pod4-leaf-4 | 100.100.4.4/32 |
| POD4_LEAFS | pod4-leaf-5 | 100.100.4.5/32 |
| POD4_LEAFS | pod4-leaf-6 | 100.100.4.6/32 |
| POD4_LEAFS | pod4-leaf-7 | 100.100.4.7/32 |
| POD4_LEAFS | pod4-leaf-8 | 100.100.4.8/32 |
| POD4_LEAFS | pod4-leaf-9 | 100.100.4.9/32 |
| POD4_LEAFS | pod4-leaf-10 | 100.100.4.10/32 |
| POD4_LEAFS | pod4-leaf-11 | 100.100.4.11/32 |
| POD4_LEAFS | pod4-leaf-12 | 100.100.4.12/32 |
| POD4_LEAFS | pod4-leaf-13 | 100.100.4.13/32 |
| POD4_LEAFS | pod4-leaf-14 | 100.100.4.14/32 |
| POD4_LEAFS | pod4-leaf-15 | 100.100.4.15/32 |
| POD4_LEAFS | pod4-leaf-16 | 100.100.4.16/32 |
| POD4_LEAFS | pod4-leaf-17 | 100.100.4.17/32 |
| POD4_LEAFS | pod4-leaf-18 | 100.100.4.18/32 |
| POD4_LEAFS | pod4-leaf-19 | 100.100.4.19/32 |
| POD4_LEAFS | pod4-leaf-20 | 100.100.4.20/32 |
| POD4_LEAFS | pod4-leaf-21 | 100.100.4.21/32 |
| POD4_LEAFS | pod4-leaf-22 | 100.100.4.22/32 |
| POD4_LEAFS | pod4-leaf-23 | 100.100.4.23/32 |
| POD4_LEAFS | pod4-leaf-24 | 100.100.4.24/32 |
| POD4_LEAFS | pod4-leaf-25 | 100.100.4.25/32 |
| POD4_LEAFS | pod4-leaf-26 | 100.100.4.26/32 |
| FABRIC | pod4-spine-1 | 100.100.7.7/32 |
| FABRIC | pod4-spine-2 | 100.100.7.8/32 |
| FABRIC | services-leaf-1 | 100.100.5.17/32 |
| FABRIC | services-leaf-2 | 100.100.5.18/32 |
| FABRIC | super-spine-1 | 100.100.6.1/32 |
| FABRIC | super-spine-2 | 100.100.6.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |
| 10.100.1.0/24 | 256 | 16 | 6.25 % |
| 10.100.2.0/24 | 256 | 16 | 6.25 % |
| 10.100.3.0/24 | 256 | 4 | 1.57 % |
| 10.100.4.0/24 | 256 | 26 | 10.16 % |
| 10.100.5.0/24 | 256 | 2 | 0.79 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| POD1_LEAFS | pod1-leaf-1 | 10.100.1.1/32 |
| POD1_LEAFS | pod1-leaf-2 | 10.100.1.1/32 |
| POD1_LEAFS | pod1-leaf-3 | 10.100.1.3/32 |
| POD1_LEAFS | pod1-leaf-4 | 10.100.1.3/32 |
| POD1_LEAFS | pod1-leaf-5 | 10.100.1.5/32 |
| POD1_LEAFS | pod1-leaf-6 | 10.100.1.5/32 |
| POD1_LEAFS | pod1-leaf-7 | 10.100.1.7/32 |
| POD1_LEAFS | pod1-leaf-8 | 10.100.1.7/32 |
| POD1_LEAFS | pod1-leaf-9 | 10.100.1.9/32 |
| POD1_LEAFS | pod1-leaf-10 | 10.100.1.9/32 |
| POD1_LEAFS | pod1-leaf-11 | 10.100.1.11/32 |
| POD1_LEAFS | pod1-leaf-12 | 10.100.1.11/32 |
| POD1_LEAFS | pod1-leaf-13 | 10.100.1.13/32 |
| POD1_LEAFS | pod1-leaf-14 | 10.100.1.13/32 |
| POD1_LEAFS | pod1-leaf-15 | 10.100.1.15/32 |
| POD1_LEAFS | pod1-leaf-16 | 10.100.1.15/32 |
| POD2_LEAFS | pod2-leaf-1 | 10.100.2.1/32 |
| POD2_LEAFS | pod2-leaf-2 | 10.100.2.1/32 |
| POD2_LEAFS | pod2-leaf-3 | 10.100.2.3/32 |
| POD2_LEAFS | pod2-leaf-4 | 10.100.2.3/32 |
| POD2_LEAFS | pod2-leaf-5 | 10.100.2.5/32 |
| POD2_LEAFS | pod2-leaf-6 | 10.100.2.5/32 |
| POD2_LEAFS | pod2-leaf-7 | 10.100.2.7/32 |
| POD2_LEAFS | pod2-leaf-8 | 10.100.2.7/32 |
| POD2_LEAFS | pod2-leaf-9 | 10.100.2.9/32 |
| POD2_LEAFS | pod2-leaf-10 | 10.100.2.9/32 |
| POD2_LEAFS | pod2-leaf-11 | 10.100.2.11/32 |
| POD2_LEAFS | pod2-leaf-12 | 10.100.2.11/32 |
| POD2_LEAFS | pod2-leaf-13 | 10.100.2.13/32 |
| POD2_LEAFS | pod2-leaf-14 | 10.100.2.13/32 |
| POD2_LEAFS | pod2-leaf-15 | 10.100.2.15/32 |
| POD2_LEAFS | pod2-leaf-16 | 10.100.2.15/32 |
| POD3_LEAFS | pod3-leaf-1 | 10.100.3.1/32 |
| POD3_LEAFS | pod3-leaf-2 | 10.100.3.1/32 |
| POD3_LEAFS | pod3-leaf-3 | 10.100.3.3/32 |
| POD3_LEAFS | pod3-leaf-4 | 10.100.3.3/32 |
| POD4_LEAFS | pod4-leaf-1 | 10.100.4.1/32 |
| POD4_LEAFS | pod4-leaf-2 | 10.100.4.1/32 |
| POD4_LEAFS | pod4-leaf-3 | 10.100.4.3/32 |
| POD4_LEAFS | pod4-leaf-4 | 10.100.4.3/32 |
| POD4_LEAFS | pod4-leaf-5 | 10.100.4.5/32 |
| POD4_LEAFS | pod4-leaf-6 | 10.100.4.5/32 |
| POD4_LEAFS | pod4-leaf-7 | 10.100.4.7/32 |
| POD4_LEAFS | pod4-leaf-8 | 10.100.4.7/32 |
| POD4_LEAFS | pod4-leaf-9 | 10.100.4.9/32 |
| POD4_LEAFS | pod4-leaf-10 | 10.100.4.9/32 |
| POD4_LEAFS | pod4-leaf-11 | 10.100.4.11/32 |
| POD4_LEAFS | pod4-leaf-12 | 10.100.4.11/32 |
| POD4_LEAFS | pod4-leaf-13 | 10.100.4.13/32 |
| POD4_LEAFS | pod4-leaf-14 | 10.100.4.13/32 |
| POD4_LEAFS | pod4-leaf-15 | 10.100.4.15/32 |
| POD4_LEAFS | pod4-leaf-16 | 10.100.4.15/32 |
| POD4_LEAFS | pod4-leaf-17 | 10.100.4.17/32 |
| POD4_LEAFS | pod4-leaf-18 | 10.100.4.17/32 |
| POD4_LEAFS | pod4-leaf-19 | 10.100.4.19/32 |
| POD4_LEAFS | pod4-leaf-20 | 10.100.4.19/32 |
| POD4_LEAFS | pod4-leaf-21 | 10.100.4.21/32 |
| POD4_LEAFS | pod4-leaf-22 | 10.100.4.21/32 |
| POD4_LEAFS | pod4-leaf-23 | 10.100.4.23/32 |
| POD4_LEAFS | pod4-leaf-24 | 10.100.4.23/32 |
| POD4_LEAFS | pod4-leaf-25 | 10.100.4.25/32 |
| POD4_LEAFS | pod4-leaf-26 | 10.100.4.25/32 |
| FABRIC | services-leaf-1 | 10.100.5.17/32 |
| FABRIC | services-leaf-2 | 10.100.5.17/32 |
