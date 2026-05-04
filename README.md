# OSPF Multi Area Network Design and Validation Across Large Scale Topology

## Overview
Designed and implemented a large scale routed network using OSPF across multiple areas. Configured 16 routers to establish dynamic routing between two distant LAN segments and validated end to end connectivity. Extended the design to include multi area OSPF with Area Border Routers and verified inter area communication through troubleshooting and correction of area misconfiguration.

## Objective
Implemented OSPF based routing across a multi router topology to enable scalable communication between networks. Designed multi area segmentation using backbone and non backbone areas and validated routing behavior through controlled testing and troubleshooting.

## Network Setup
Devices Used
- 16 Routers
- 2 Switches
- 2 End Devices PCs
```
Topology Design
PC0 connected to Router0
PC1 connected to Router16
Routers connected in series forming a long path between endpoints
```
LAN Networks
- PC0 Address 192.168.1.10
- Router0 Interface 192.168.1.1


- PC1 Address 192.168.2.10
- Router16 Interface 192.168.2.1


Logical Flow
PC0 to Router0 through OSPF domain across all routers to Router16 to PC1

Topology and OSPF Convergence
![OSPF Full Topology](https://github.com/Pelumi-Johnson/OSPF-Multi-Area-Network-Design-and-Validation-Across-Large-Scale-Topology/blob/main/Screenshot%202026-05-04%20002509.png)

---

## Configuration

### Base OSPF Configuration Single Area

Configured OSPF across all routers within Area 0 to establish baseline connectivity
```
router ospf 1
network 192.168.x.x 0.0.0.255 area 0
network 200.1.x.x 0.0.0.255 area 0
```
Applied appropriate network statements per interface on each router

Video Placeholder Initial OSPF Configuration
![OSPF Area0](./videos/ospf-area0.mp4)

---

### End to End Connectivity Validation

Tested communication from PC0 to PC1
```
ping 192.168.2.10
```
Result successful confirming full OSPF adjacency and routing table propagation across all routers

Video Placeholder Successful End to End Ping
![OSPF Ping Success](./videos/ospf-ping-success.mp4)

---

### Routing and Neighbor Verification

Verified OSPF route propagation and adjacency formation
```
show ip route
```
Observation
Routing table on Router0 displayed all learned networks across the topology confirming successful route advertisement through OSPF
```
show ip ospf neighbor
```
Observation
Neighbor relationships established across connected routers confirming full OSPF adjacency

Video Placeholder Routing Table and Neighbor Verification
![OSPF Verification](./videos/ospf-verification.mp4)

---

## Multi Area OSPF Design

### Area Segmentation

Modified topology to introduce multiple OSPF areas
```
Router0 interfaces assigned to Area 1
Router1 interface facing Router0 assigned to Area 1

Remaining interfaces of Router1 remained in Area 0 making Router1 an Area Border Router

Router16 interfaces assigned to Area 2
Router15 interface facing Router16 assigned to Area 2

Remaining interfaces of Router15 remained in Area 0 making Router15 an Area Border Router
```
Video Placeholder Multi Area Configuration
![OSPF Multi Area](./videos/ospf-multi-area.mp4)

---

## Failure Scenario

### Misconfiguration Encountered

Incorrectly advertised network 192.168.1.0 in Area 0 on Router16

Result
OSPF routing inconsistency between areas
End to end communication failed

ping 192.168.2.10

Result request timed out confirming routing failure

Video Placeholder OSPF Failure
![OSPF Failure](./videos/ospf-failure.mp4)

---

## Troubleshooting and Resolution

### Diagnosis

Reviewed OSPF configuration across edge routers
Identified incorrect area assignment on Router16
```
show running-config
```
Confirmed mismatch between network advertisement and intended area design

### Fix Applied

Removed incorrect network statement from Area 0 on Router16
Reassigned correct network to Area 2
```
no router ospf 1

```
### Validation

Retested connectivity
```
ping 192.168.2.10
```
Result successful confirming proper inter area routing through backbone

Video Placeholder OSPF Fix and Recovery
![OSPF Fix](./videos/ospf-fix.mp4)

---

## Key Concepts Applied
- OSPF dynamic routing across multi hop topology
- Single area OSPF for baseline connectivity
- Multi area OSPF design using backbone Area 0
- Area Border Router configuration for inter area communication
- Route advertisement consistency across areas
- OSPF neighbor adjacency verification
- Routing table validation using show commands
- End to end verification of routing convergence

## Outcome
Successfully implemented a large scale OSPF network enabling communication across 16 routers. Designed and validated multi area routing using Area Border Routers and backbone area principles. Verified routing tables and neighbor relationships to confirm proper convergence. Identified and resolved routing failure caused by incorrect area advertisement, restoring full connectivity and demonstrating real world routing design and troubleshooting capability.
