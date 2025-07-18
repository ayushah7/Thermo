# pod1-spine-1

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
| Management1 | OOB_MANAGEMENT | oob | MGMT | 192.168.0.201/24 | - |

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
   ip address 192.168.0.201/24
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 8.8.8.8 | MGMT | - |
| 8.8.4.4 | MGMT | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf MGMT 8.8.4.4
ip name-server vrf MGMT 8.8.8.8
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 1.north-america.pool.ntp.org | MGMT | True | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server vrf MGMT 1.north-america.pool.ntp.org prefer
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
| Ethernet1 | P2P_super-spine-1_Ethernet1 | - | 10.255.250.1/31 | default | 1500 | False | - | - |
| Ethernet2 | P2P_super-spine-2_Ethernet1 | - | 10.255.250.3/31 | default | 1500 | False | - | - |
| Ethernet3 | P2P_pod1-leaf-1_Ethernet1 | - | 10.255.255.0/31 | default | 1500 | False | - | - |
| Ethernet4 | P2P_pod1-leaf-2_Ethernet1 | - | 10.255.255.4/31 | default | 1500 | False | - | - |
| Ethernet5 | P2P_pod1-leaf-3_Ethernet1 | - | 10.255.255.8/31 | default | 1500 | False | - | - |
| Ethernet6 | P2P_pod1-leaf-4_Ethernet1 | - | 10.255.255.12/31 | default | 1500 | False | - | - |
| Ethernet7 | P2P_pod1-leaf-5_Ethernet1 | - | 10.255.255.16/31 | default | 1500 | False | - | - |
| Ethernet8 | P2P_pod1-leaf-6_Ethernet1 | - | 10.255.255.20/31 | default | 1500 | False | - | - |
| Ethernet9 | P2P_pod1-leaf-7_Ethernet1 | - | 10.255.255.24/31 | default | 1500 | False | - | - |
| Ethernet10 | P2P_pod1-leaf-8_Ethernet1 | - | 10.255.255.28/31 | default | 1500 | False | - | - |
| Ethernet11 | P2P_pod1-leaf-9_Ethernet1 | - | 10.255.255.32/31 | default | 1500 | False | - | - |
| Ethernet12 | P2P_pod1-leaf-10_Ethernet1 | - | 10.255.255.36/31 | default | 1500 | False | - | - |
| Ethernet13 | P2P_pod1-leaf-11_Ethernet1 | - | 10.255.255.40/31 | default | 1500 | False | - | - |
| Ethernet14 | P2P_pod1-leaf-12_Ethernet1 | - | 10.255.255.44/31 | default | 1500 | False | - | - |
| Ethernet15 | P2P_pod1-leaf-13_Ethernet1 | - | 10.255.255.48/31 | default | 1500 | False | - | - |
| Ethernet16 | P2P_pod1-leaf-14_Ethernet1 | - | 10.255.255.52/31 | default | 1500 | False | - | - |
| Ethernet17 | P2P_pod1-leaf-15_Ethernet1 | - | 10.255.255.56/31 | default | 1500 | False | - | - |
| Ethernet18 | P2P_pod1-leaf-16_Ethernet1 | - | 10.255.255.60/31 | default | 1500 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_super-spine-1_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.1/31
!
interface Ethernet2
   description P2P_super-spine-2_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.250.3/31
!
interface Ethernet3
   description P2P_pod1-leaf-1_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.0/31
!
interface Ethernet4
   description P2P_pod1-leaf-2_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.4/31
!
interface Ethernet5
   description P2P_pod1-leaf-3_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.8/31
!
interface Ethernet6
   description P2P_pod1-leaf-4_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.12/31
!
interface Ethernet7
   description P2P_pod1-leaf-5_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.16/31
!
interface Ethernet8
   description P2P_pod1-leaf-6_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.20/31
!
interface Ethernet9
   description P2P_pod1-leaf-7_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.24/31
!
interface Ethernet10
   description P2P_pod1-leaf-8_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.28/31
!
interface Ethernet11
   description P2P_pod1-leaf-9_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.32/31
!
interface Ethernet12
   description P2P_pod1-leaf-10_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.36/31
!
interface Ethernet13
   description P2P_pod1-leaf-11_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.40/31
!
interface Ethernet14
   description P2P_pod1-leaf-12_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.44/31
!
interface Ethernet15
   description P2P_pod1-leaf-13_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.48/31
!
interface Ethernet16
   description P2P_pod1-leaf-14_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.52/31
!
interface Ethernet17
   description P2P_pod1-leaf-15_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.56/31
!
interface Ethernet18
   description P2P_pod1-leaf-16_Ethernet1
   no shutdown
   mtu 1500
   no switchport
   ip address 10.255.255.60/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 100.104.0.1/32 |

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
   ip address 100.104.0.1/32
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
| 65150 | 100.104.0.1 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 10.255.250.0 | 65000 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.250.2 | 65000 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.1 | 65101 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.5 | 65101 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.9 | 65102 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.13 | 65102 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.17 | 65103 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.21 | 65103 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.25 | 65104 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.29 | 65104 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.33 | 65105 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.37 | 65105 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.41 | 65106 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.45 | 65106 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.49 | 65107 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.53 | 65107 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.57 | 65108 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.61 | 65108 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65150
   router-id 100.104.0.1
   no bgp default ipv4-unicast
   maximum-paths 4 ecmp 4
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 <removed>
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 10.255.250.0 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.0 remote-as 65000
   neighbor 10.255.250.0 description super-spine-1_Ethernet1
   neighbor 10.255.250.2 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.250.2 remote-as 65000
   neighbor 10.255.250.2 description super-spine-2_Ethernet1
   neighbor 10.255.255.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.1 remote-as 65101
   neighbor 10.255.255.1 description pod1-leaf-1_Ethernet1
   neighbor 10.255.255.5 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.5 remote-as 65101
   neighbor 10.255.255.5 description pod1-leaf-2_Ethernet1
   neighbor 10.255.255.9 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.9 remote-as 65102
   neighbor 10.255.255.9 description pod1-leaf-3_Ethernet1
   neighbor 10.255.255.13 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.13 remote-as 65102
   neighbor 10.255.255.13 description pod1-leaf-4_Ethernet1
   neighbor 10.255.255.17 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.17 remote-as 65103
   neighbor 10.255.255.17 description pod1-leaf-5_Ethernet1
   neighbor 10.255.255.21 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.21 remote-as 65103
   neighbor 10.255.255.21 description pod1-leaf-6_Ethernet1
   neighbor 10.255.255.25 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.25 remote-as 65104
   neighbor 10.255.255.25 description pod1-leaf-7_Ethernet1
   neighbor 10.255.255.29 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.29 remote-as 65104
   neighbor 10.255.255.29 description pod1-leaf-8_Ethernet1
   neighbor 10.255.255.33 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.33 remote-as 65105
   neighbor 10.255.255.33 description pod1-leaf-9_Ethernet1
   neighbor 10.255.255.37 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.37 remote-as 65105
   neighbor 10.255.255.37 description pod1-leaf-10_Ethernet1
   neighbor 10.255.255.41 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.41 remote-as 65106
   neighbor 10.255.255.41 description pod1-leaf-11_Ethernet1
   neighbor 10.255.255.45 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.45 remote-as 65106
   neighbor 10.255.255.45 description pod1-leaf-12_Ethernet1
   neighbor 10.255.255.49 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.49 remote-as 65107
   neighbor 10.255.255.49 description pod1-leaf-13_Ethernet1
   neighbor 10.255.255.53 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.53 remote-as 65107
   neighbor 10.255.255.53 description pod1-leaf-14_Ethernet1
   neighbor 10.255.255.57 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.57 remote-as 65108
   neighbor 10.255.255.57 description pod1-leaf-15_Ethernet1
   neighbor 10.255.255.61 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.61 remote-as 65108
   neighbor 10.255.255.61 description pod1-leaf-16_Ethernet1
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family ipv4
      neighbor IPv4-UNDERLAY-PEERS activate
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 100.104.0.0/26 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 100.104.0.0/26 eq 32
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
