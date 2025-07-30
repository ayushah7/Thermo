# super-spine-2

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [EOS CLI Device Configuration](#eos-cli-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | MGMT | 192.168.0.2/24 | - |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | OOB_MANAGEMENT | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management1
   description OOB_MANAGEMENT
   no shutdown
   vrf MGMT
   ip address 192.168.0.2/24
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 8.8.8.8 | default | - |
| 8.8.4.4 | default | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf default 8.8.4.4
ip name-server vrf default 8.8.8.8
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 0.north-america.pool.ntp.org | default | False | - | - | - | - | - | - | - |
| 1.north-america.pool.ntp.org | default | True | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server 0.north-america.pool.ntp.org
ntp server 1.north-america.pool.ntp.org prefer
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | UNIX-Socket | Default Services |
| ---- | ----- | ----------- | ---------------- |
| False | True | - | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| default | - | - |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf default
      no shutdown
   !
   vrf MGMT
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| ansible | 15 | network-admin | False | - |
| cvpadmin | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username ansible privilege 15 role network-admin secret sha512 <removed>
username cvpadmin privilege 15 role network-admin secret sha512 <removed>
```

### Enable Password

Enable password has been disabled

## Monitoring

### TerminAttr Daemon

#### TerminAttr Daemon Summary

| CV Compression | CloudVision Servers | VRF | Authentication | Smash Excludes | Ingest Exclude | Bypass AAA |
| -------------- | ------------------- | --- | -------------- | -------------- | -------------- | ---------- |
| gzip | 192.168.0.5:9910 | MGMT | token,/tmp/token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | True |

#### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=192.168.0.5:9910 -cvauth=token,/tmp/token -cvvrf=MGMT -disableaaa -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **none**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_pod1-spine-1_Ethernet2 | - | 10.255.250.2/31 | default | 1500 | False | - | - |
| Ethernet2 | P2P_pod1-spine-2_Ethernet2 | - | 10.255.250.6/31 | default | 1500 | False | - | - |
| Ethernet3 | P2P_pod2-spine-1_Ethernet2 | - | 10.255.250.10/31 | default | 1500 | False | - | - |
| Ethernet4 | P2P_pod2-spine-2_Ethernet2 | - | 10.255.250.14/31 | default | 1500 | False | - | - |
| Ethernet5 | P2P_pod3-spine-1_Ethernet2 | - | 10.255.250.18/31 | default | 1500 | False | - | - |
| Ethernet6 | P2P_pod3-spine-2_Ethernet2 | - | 10.255.250.22/31 | default | 1500 | False | - | - |
| Ethernet7 | P2P_pod4-spine-1_Ethernet2 | - | 10.255.250.26/31 | default | 1500 | False | - | - |
| Ethernet8 | P2P_pod4-spine-2_Ethernet2 | - | 10.255.250.30/31 | default | 1500 | False | - | - |
| Ethernet17 | P2P_services-leaf-1_Ethernet2 | - | 10.255.251.66/31 | default | 1500 | False | - | - |
| Ethernet18 | P2P_services-leaf-2_Ethernet2 | - | 10.255.251.70/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_pod1-spine-1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.2/31
!
interface Ethernet2
   description P2P_pod1-spine-2_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.6/31
!
interface Ethernet3
   description P2P_pod2-spine-1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.10/31
!
interface Ethernet4
   description P2P_pod2-spine-2_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.14/31
!
interface Ethernet5
   description P2P_pod3-spine-1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.18/31
!
interface Ethernet6
   description P2P_pod3-spine-2_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.22/31
!
interface Ethernet7
   description P2P_pod4-spine-1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.26/31
!
interface Ethernet8
   description P2P_pod4-spine-2_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.30/31
!
interface Ethernet17
   description P2P_services-leaf-1_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.251.66/31
!
interface Ethernet18
   description P2P_services-leaf-2_Ethernet2
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.251.70/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 100.100.6.2/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 100.100.6.2/32
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65000 | 100.100.6.2 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 10.255.250.3 | 65000.15 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.7 | 65000.15 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.11 | 65000.151 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.15 | 65000.151 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.19 | 65000.152 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.23 | 65000.152 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.27 | 65000.153 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.31 | 65000.153 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.251.67 | 65200 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.251.71 | 65200 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 100.100.1.1 | 65000.101 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.2 | 65000.101 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.3 | 65000.102 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.4 | 65000.102 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.5 | 65000.103 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.6 | 65000.103 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.7 | 65000.104 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.8 | 65000.104 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.9 | 65000.105 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.10 | 65000.105 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.11 | 65000.106 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.12 | 65000.106 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.13 | 65000.107 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.14 | 65000.107 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.15 | 65000.108 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.1.16 | 65000.108 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.1 | 65000.133 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.2 | 65000.133 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.3 | 65000.134 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.4 | 65000.134 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.5 | 65000.135 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.6 | 65000.135 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.7 | 65000.136 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.8 | 65000.136 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.9 | 65000.137 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.10 | 65000.137 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.11 | 65000.138 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.12 | 65000.138 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.13 | 65000.139 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.14 | 65000.139 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.15 | 65000.14 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.2.16 | 65000.14 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.3.1 | 65000.105 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.3.2 | 65000.105 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.3.3 | 65000.106 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.3.4 | 65000.106 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.1 | 65000.109 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.2 | 65000.109 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.3 | 65000.11 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.4 | 65000.11 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.5 | 65000.111 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.6 | 65000.111 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.7 | 65000.112 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.8 | 65000.112 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.9 | 65000.113 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.10 | 65000.113 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.11 | 65000.114 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.12 | 65000.114 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.13 | 65000.115 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.14 | 65000.115 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.15 | 65000.116 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.16 | 65000.116 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.17 | 65000.117 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.18 | 65000.117 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.19 | 65000.118 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.20 | 65000.118 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.21 | 65000.119 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.22 | 65000.119 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.23 | 65000.12 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.24 | 65000.12 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.25 | 65000.121 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.4.26 | 65000.121 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.5.17 | 65200 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 100.100.5.18 | 65200 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ------------- | ------------------------------ |
| EVPN-OVERLAY-PEERS | True |  - | - | default | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65000
   router-id 100.100.6.2
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 <removed>
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 <removed>
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 10.255.250.3 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.3 remote-as 65000.15
   neighbor 10.255.250.3 description pod1-spine-1_Ethernet2
   neighbor 10.255.250.7 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.7 remote-as 65000.15
   neighbor 10.255.250.7 description pod1-spine-2_Ethernet2
   neighbor 10.255.250.11 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.11 remote-as 65000.151
   neighbor 10.255.250.11 description pod2-spine-1_Ethernet2
   neighbor 10.255.250.15 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.15 remote-as 65000.151
   neighbor 10.255.250.15 description pod2-spine-2_Ethernet2
   neighbor 10.255.250.19 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.19 remote-as 65000.152
   neighbor 10.255.250.19 description pod3-spine-1_Ethernet2
   neighbor 10.255.250.23 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.23 remote-as 65000.152
   neighbor 10.255.250.23 description pod3-spine-2_Ethernet2
   neighbor 10.255.250.27 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.27 remote-as 65000.153
   neighbor 10.255.250.27 description pod4-spine-1_Ethernet2
   neighbor 10.255.250.31 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.31 remote-as 65000.153
   neighbor 10.255.250.31 description pod4-spine-2_Ethernet2
   neighbor 10.255.251.67 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.251.67 remote-as 65200
   neighbor 10.255.251.67 description services-leaf-1_Ethernet2
   neighbor 10.255.251.71 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.251.71 remote-as 65200
   neighbor 10.255.251.71 description services-leaf-2_Ethernet2
   neighbor 100.100.1.1 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.1 remote-as 65000.101
   neighbor 100.100.1.1 description pod1-leaf-1_Loopback0
   neighbor 100.100.1.2 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.2 remote-as 65000.101
   neighbor 100.100.1.2 description pod1-leaf-2_Loopback0
   neighbor 100.100.1.3 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.3 remote-as 65000.102
   neighbor 100.100.1.3 description pod1-leaf-3_Loopback0
   neighbor 100.100.1.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.4 remote-as 65000.102
   neighbor 100.100.1.4 description pod1-leaf-4_Loopback0
   neighbor 100.100.1.5 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.5 remote-as 65000.103
   neighbor 100.100.1.5 description pod1-leaf-5_Loopback0
   neighbor 100.100.1.6 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.6 remote-as 65000.103
   neighbor 100.100.1.6 description pod1-leaf-6_Loopback0
   neighbor 100.100.1.7 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.7 remote-as 65000.104
   neighbor 100.100.1.7 description pod1-leaf-7_Loopback0
   neighbor 100.100.1.8 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.8 remote-as 65000.104
   neighbor 100.100.1.8 description pod1-leaf-8_Loopback0
   neighbor 100.100.1.9 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.9 remote-as 65000.105
   neighbor 100.100.1.9 description pod1-leaf-9_Loopback0
   neighbor 100.100.1.10 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.10 remote-as 65000.105
   neighbor 100.100.1.10 description pod1-leaf-10_Loopback0
   neighbor 100.100.1.11 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.11 remote-as 65000.106
   neighbor 100.100.1.11 description pod1-leaf-11_Loopback0
   neighbor 100.100.1.12 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.12 remote-as 65000.106
   neighbor 100.100.1.12 description pod1-leaf-12_Loopback0
   neighbor 100.100.1.13 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.13 remote-as 65000.107
   neighbor 100.100.1.13 description pod1-leaf-13_Loopback0
   neighbor 100.100.1.14 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.14 remote-as 65000.107
   neighbor 100.100.1.14 description pod1-leaf-14_Loopback0
   neighbor 100.100.1.15 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.15 remote-as 65000.108
   neighbor 100.100.1.15 description pod1-leaf-15_Loopback0
   neighbor 100.100.1.16 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.1.16 remote-as 65000.108
   neighbor 100.100.1.16 description pod1-leaf-16_Loopback0
   neighbor 100.100.2.1 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.1 remote-as 65000.133
   neighbor 100.100.2.1 description pod2-leaf-1_Loopback0
   neighbor 100.100.2.2 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.2 remote-as 65000.133
   neighbor 100.100.2.2 description pod2-leaf-2_Loopback0
   neighbor 100.100.2.3 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.3 remote-as 65000.134
   neighbor 100.100.2.3 description pod2-leaf-3_Loopback0
   neighbor 100.100.2.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.4 remote-as 65000.134
   neighbor 100.100.2.4 description pod2-leaf-4_Loopback0
   neighbor 100.100.2.5 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.5 remote-as 65000.135
   neighbor 100.100.2.5 description pod2-leaf-5_Loopback0
   neighbor 100.100.2.6 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.6 remote-as 65000.135
   neighbor 100.100.2.6 description pod2-leaf-6_Loopback0
   neighbor 100.100.2.7 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.7 remote-as 65000.136
   neighbor 100.100.2.7 description pod2-leaf-7_Loopback0
   neighbor 100.100.2.8 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.8 remote-as 65000.136
   neighbor 100.100.2.8 description pod2-leaf-8_Loopback0
   neighbor 100.100.2.9 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.9 remote-as 65000.137
   neighbor 100.100.2.9 description pod2-leaf-9_Loopback0
   neighbor 100.100.2.10 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.10 remote-as 65000.137
   neighbor 100.100.2.10 description pod2-leaf-10_Loopback0
   neighbor 100.100.2.11 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.11 remote-as 65000.138
   neighbor 100.100.2.11 description pod2-leaf-11_Loopback0
   neighbor 100.100.2.12 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.12 remote-as 65000.138
   neighbor 100.100.2.12 description pod2-leaf-12_Loopback0
   neighbor 100.100.2.13 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.13 remote-as 65000.139
   neighbor 100.100.2.13 description pod2-leaf-13_Loopback0
   neighbor 100.100.2.14 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.14 remote-as 65000.139
   neighbor 100.100.2.14 description pod2-leaf-14_Loopback0
   neighbor 100.100.2.15 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.15 remote-as 65000.14
   neighbor 100.100.2.15 description pod2-leaf-15_Loopback0
   neighbor 100.100.2.16 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.2.16 remote-as 65000.14
   neighbor 100.100.2.16 description pod2-leaf-16_Loopback0
   neighbor 100.100.3.1 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.3.1 remote-as 65000.105
   neighbor 100.100.3.1 description pod3-leaf-1_Loopback0
   neighbor 100.100.3.2 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.3.2 remote-as 65000.105
   neighbor 100.100.3.2 description pod3-leaf-2_Loopback0
   neighbor 100.100.3.3 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.3.3 remote-as 65000.106
   neighbor 100.100.3.3 description pod3-leaf-3_Loopback0
   neighbor 100.100.3.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.3.4 remote-as 65000.106
   neighbor 100.100.3.4 description pod3-leaf-4_Loopback0
   neighbor 100.100.4.1 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.1 remote-as 65000.109
   neighbor 100.100.4.1 description pod4-leaf-1_Loopback0
   neighbor 100.100.4.2 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.2 remote-as 65000.109
   neighbor 100.100.4.2 description pod4-leaf-2_Loopback0
   neighbor 100.100.4.3 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.3 remote-as 65000.11
   neighbor 100.100.4.3 description pod4-leaf-3_Loopback0
   neighbor 100.100.4.4 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.4 remote-as 65000.11
   neighbor 100.100.4.4 description pod4-leaf-4_Loopback0
   neighbor 100.100.4.5 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.5 remote-as 65000.111
   neighbor 100.100.4.5 description pod4-leaf-5_Loopback0
   neighbor 100.100.4.6 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.6 remote-as 65000.111
   neighbor 100.100.4.6 description pod4-leaf-6_Loopback0
   neighbor 100.100.4.7 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.7 remote-as 65000.112
   neighbor 100.100.4.7 description pod4-leaf-7_Loopback0
   neighbor 100.100.4.8 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.8 remote-as 65000.112
   neighbor 100.100.4.8 description pod4-leaf-8_Loopback0
   neighbor 100.100.4.9 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.9 remote-as 65000.113
   neighbor 100.100.4.9 description pod4-leaf-9_Loopback0
   neighbor 100.100.4.10 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.10 remote-as 65000.113
   neighbor 100.100.4.10 description pod4-leaf-10_Loopback0
   neighbor 100.100.4.11 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.11 remote-as 65000.114
   neighbor 100.100.4.11 description pod4-leaf-11_Loopback0
   neighbor 100.100.4.12 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.12 remote-as 65000.114
   neighbor 100.100.4.12 description pod4-leaf-12_Loopback0
   neighbor 100.100.4.13 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.13 remote-as 65000.115
   neighbor 100.100.4.13 description pod4-leaf-13_Loopback0
   neighbor 100.100.4.14 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.14 remote-as 65000.115
   neighbor 100.100.4.14 description pod4-leaf-14_Loopback0
   neighbor 100.100.4.15 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.15 remote-as 65000.116
   neighbor 100.100.4.15 description pod4-leaf-15_Loopback0
   neighbor 100.100.4.16 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.16 remote-as 65000.116
   neighbor 100.100.4.16 description pod4-leaf-16_Loopback0
   neighbor 100.100.4.17 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.17 remote-as 65000.117
   neighbor 100.100.4.17 description pod4-leaf-17_Loopback0
   neighbor 100.100.4.18 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.18 remote-as 65000.117
   neighbor 100.100.4.18 description pod4-leaf-18_Loopback0
   neighbor 100.100.4.19 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.19 remote-as 65000.118
   neighbor 100.100.4.19 description pod4-leaf-19_Loopback0
   neighbor 100.100.4.20 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.20 remote-as 65000.118
   neighbor 100.100.4.20 description pod4-leaf-20_Loopback0
   neighbor 100.100.4.21 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.21 remote-as 65000.119
   neighbor 100.100.4.21 description pod4-leaf-21_Loopback0
   neighbor 100.100.4.22 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.22 remote-as 65000.119
   neighbor 100.100.4.22 description pod4-leaf-22_Loopback0
   neighbor 100.100.4.23 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.23 remote-as 65000.12
   neighbor 100.100.4.23 description pod4-leaf-23_Loopback0
   neighbor 100.100.4.24 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.24 remote-as 65000.12
   neighbor 100.100.4.24 description pod4-leaf-24_Loopback0
   neighbor 100.100.4.25 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.25 remote-as 65000.121
   neighbor 100.100.4.25 description pod4-leaf-25_Loopback0
   neighbor 100.100.4.26 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.4.26 remote-as 65000.121
   neighbor 100.100.4.26 description pod4-leaf-26_Loopback0
   neighbor 100.100.5.17 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.5.17 remote-as 65200
   neighbor 100.100.5.17 description services-leaf-1_Loopback0
   neighbor 100.100.5.18 peer group EVPN-OVERLAY-PEERS
   neighbor 100.100.5.18 remote-as 65200
   neighbor 100.100.5.18 description services-leaf-2_Loopback0
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 100.100.6.0/26 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 100.100.6.0/26 eq 32
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

## EOS CLI Device Configuration

```eos
!
no aaa root
no username admin
username cwomble secret *
aaa authorization exec default local
username cwomble ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDOZFQIhHNghkuJryYiNyFUbkVPyGH2tU1gFuoJ/wDDg420VY9tb1OQn7k+XoDaVWWoEoOek07sJzns0Yy7WYUhgHP3T8Q3qW2DRjRDCUgUXnt9iW9N/axh4U4OP71UbWJNw3D6b5JE4EWt56okFcR6eSAyyKoYZvUAiCX1oUGVbRDz0cTNTbbnYHXp8DFBM/3fLNrO7Ntif+1ZtY8IQoZoDaOZpQLqTt40QGBAJgyXy0xP3urSaSJP2alSZP0g2IY9WebHaJAKnzP+SCuU4pMpcWYE3EoevYB6RLy12WylXq7Ht8sy2cjB9HH19BM4lNvRJ7ArjsL8enBP4OdqdyCH/SfLy6YrQ2EFidNpxnGBNVxIA7lkK82jLGFiqKJJNapZW4nRljT+KVMFEh/NTDP61wYmUPCR331+e3TiKsapwcIN/Q1+20WBVf11RseChjLqZzu54y9PDw/MA8ra8mPbuenhNJ6Xw8nkZbeUr+o/jZHwTP0sTLFyv4uJKvOACBc=
username ec2-user shell /bin/bash nopassword
username ec2-user ssh-key ssh-rsa ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDBzWRoRn12EsQtIEXKKKuDcut8X/vvpIan3gAZ1LI/w45s/wxBikXWTRirOavYth7h7/wrTSoBYlbr27rLa8pBUwtHIUk+5n1WuTV7S/ZHB56y3qz033AdoyRnPK2IWx6aq8CYQMB4NIqOK9/LYWTtA8Gih4KWqZhf9u+QSqGmFP6g+zW3ztKxjrmWvPD2t3DPB6U6ghfTpiJusL9zkgVCcZFgyGqtmy9Kl+qf51bQLIoT0FrsRi6M7lNr5LHo68Zi0g2krDajibJVecZAVa8oBgHj5Nu/W8jffDxM3irR7bL5M/o4YwhlVNsPLWQMof7lh92QTD4ggZcNDyzOOpQ/U5l8SEGf6poy2Kv6zTvc4WDhadJK/G8naZvt+m5/wy24d6ve1OImlRRgHi7H9ATEYE5EG6kr2JoACk1JNKA0WK6y+Ic1OkAGuq/d6u9XUKjMHNQnxynikFUeDXn9OQ3wjr5ddHZ8G2SGp1L4qxDi13cMmRWJjnM30GXh+LhO2Ps= nonroot@buildkitsandbox
username gcp-user secret *
username gcp-user ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGPEoZ2l67eEEwrlGfBAHPMx44IoqhyfjqXj2Ka4PxLuHgi1mv131VuCRlyWjOjddccyFUilfR1Bprdmd1Tj7o4Q11YQ138LOqFWJT3h0pxgHFdIHo70y4rI8aL15ixukZYa+g9KX8qTN+ZpFfea2d3CEFzMp+Y3xVPiWwLKzalq1JwT5J4MK2VHCbcnpN3zRON+gca/iZH9upA0WaXWJXNBnYXrgXFVGCJFk6Yl1ZXIGnEcKGe44c77zWgF4C66VhltsW999XD5vF31f6TTs25qxGScsiKMDg2uM1AzVg5KfxxhVy5HKd23YJJMytvUXL9h5Wq1HEEluSCcFtNI81
username mircea secret *
username mircea ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDw26o1dbfin+wgiYhiHybYebcYlS1EpucVdzfZASTkaMnCiaGy61mLtCaiZA82MEMNbkHLr9WgO2f9pHN2fiIiJc2gmlZPAUvSDzOHQapGuWzoPbeoKTaPyEzkDD5IzerV8wgMooaJOIWU9dWRjVPpUyj2GJ3JirC3HiLRnhkHFh3F+vUkEL81lMzJ/0HdnW3WrIjU6JnuOnpjiJ+np1OEPSbBdANT89tzaEm87QUioPQF7hHknKFUYK2Zqh5SXR6vQaLEcIhRqlAvZyjc95vDtYFWzqrdrHTdznyr8Hs/R2OeLmPGArGm6V8sGC9Q1bGfbhwjxvoWH9igUO6d82HKL2h8PJ1gXJU4XCb6Dkft7y0M4CDx6tIOo9jDxwFRtim9oC0uwxsRoXL4xCDYGH+jO4RAQSVxP6MQsJBEOvXez6whUev1lR91CiXmtUwQfzfmol03U8xMsBkdZ+Y4B7AkBUIpi/+8aEbMwRACyDZJB0+FzkYuWIYpiqoQ4pwUVw8=
username service shell /bin/bash secret sha512 $6$UsyZmaoGmcp3lrqe$SywidSZARI7V5UYyfxIRCeOZBv.4COucd4lEUvuhG/E.0g0vAU2d6t25RSzdqoH2ayIAh9giILovWyCOtrsEq1
!
agent KernelFib environment KERNELFIB_PROGRAM_ALL_ECMP='true'
system l1
  unsupported speed action error
  unsupported error-correction action error

```
