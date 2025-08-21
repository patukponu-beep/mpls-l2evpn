# MPLS EVPN Lab

This lab demonstrates MPLS EVPN (Ethernet VPN) as a scalable replacement for traditional Layer 2 VPNs like VPWS and VPLS. EVPN allows multiple customers to connect across a provider MPLS backbone while maintaining separation and enabling multipoint connectivity.

### Topology

The lab consists of:

* **Provider Core:** (P1, P2) running MPLS and IGP
* **Provider Edge:** (PE1, PE2, PE3) running BGP EVPN
* **Customer Edge:** (CBT1–CBT3, ACME1–ACME3) connected through PEs via EVPN instances
* **Intermediate Switches:** Used to simulate shared access - you might have to manually create vlans 10 and 20 on these 3 switches.

Each customer (CBT, ACME) has its own bridge domain and EVPN instance.

### Features

* **MPLS Core:** Uses OSPF for routing and LDP for label distribution.
* **BGP EVPN:** Serves as the control plane for Layer 2 VPN services.
* **VLAN-based EVPN:** Instances are configured on a per-customer basis.
* **Customer Separation:** Achieved using unique **Route Distinguishers (RDs)** and **Route Targets (RTs)**.
* **End-to-End Connectivity:** Provides seamless connectivity between all customer sites.

### Requirements

* **Images:** Cisco IOSv / IOSvL2 / ISRv.
* **Emulation:** EVE-NG or GNS3.
* **Knowledge:** Basic understanding of MPLS, BGP, and EVPN concepts is recommended.

### High-Level Configuration Steps

1.  **MPLS Underlay**
    * Enable OSPF in the provider core.
    * Configure LDP for label distribution.
    * Verify MPLS forwarding is operational.

2.  **BGP EVPN Overlay**
    * Configure BGP neighbors between the PEs.
    * Enable the `address-family l2vpn evpn`.
    * Assign unique RD and RT values for each customer instance.

3.  **Bridge Domains & Service Instances**
    * Create bridge domains for each customer.
    * Bind service instances to the customer-facing interfaces.
    * Map the bridge domains to their respective EVPN instances.

4.  **Customer Edge Integration**
    * Configure subinterfaces or physical ports with service instance for CE connections.
    * Run the customer's preferred IGPs (OSPF, EIGRP) if desired.

### Verification Commands

Use these commands to validate your setup and troubleshoot issues.

**MPLS & IGP**

```bash
show mpls forwarding-table
show mpls ldp neighbor
show ip ospf neighbor

````
### BGP EVPN

```bash
show bgp l2vpn evpn summary
show bgp l2vpn evpn
show bgp l2vpn evpn route-type mac-ip
````

### EVPN & Bridge Domain

```bash
show l2vpn evpn mac
show l2vpn evpn ethernet-segment
show bridge-domain
```

### End-to-End Connectivity

```bash
ping <remote-CE-IP>
traceroute <remote-CE-IP>
show ip route
show ip eigrp neighbors
show ip ospf neighbors
```

###
