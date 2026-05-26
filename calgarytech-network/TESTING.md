# Network Testing Procedures

## Pre-Deployment Checklist
- [ ] All devices powered on and showing green status
- [ ] Trunk links established (check with `show interfaces trunk`)
- [ ] VLANs created on all switches
- [ ] DHCP pools configured on Core-1
- [ ] NAT configured on R1-Edge
- [ ] ACLs applied to appropriate interfaces

---

## Layer 2 Testing

### VLAN Verification
**On Access-SW1:**
show vlan brief
show interfaces trunk
show spanning-tree
**Expected:** VLANs 10, 60, 99 present; Trunk on Gi1/0/1

---

## Layer 3 Testing

### Inter-VLAN Routing
**On Core-1:**
show ip interface brief
show ip route
**Expected:** All VLAN SVIs up/up, routes to all VLANs

**From Sales PC (10.10.10.x):**
ping 10.10.20.5    (Engineering PC)
ping 10.10.50.10   (Server)
**Expected:** Both pings succeed

---

## DHCP Testing

**From any PC:** Select DHCP mode in IP configuration

**Verify on Core-1:**
show ip dhcp binding
**Expected:** See leases for each VLAN with correct IP ranges

---

## Security Testing

### Guest WiFi Isolation
**From Guest WiFi device (10.10.80.x):**
ping 8.8.8.8              ✓ Should succeed
ping 10.10.10.10          ✗ Should fail (ACL blocks)
ping 10.10.50.10          ✗ Should fail (ACL blocks)

**Verify on Core-1:**
show access-lists GUEST-RESTRICT

### Finance VLAN Restrictions
**From Finance PC (10.10.30.x):**
ping 10.10.50.10          ✓ Should succeed (Server access)
ping 10.10.10.10          ✗ Should fail (No Sales access)

**Verify on Core-1:**
show access-lists FINANCE-RESTRICT

---

## NAT/Internet Testing

**From any internal PC:**
ping 8.8.8.8
tracert 8.8.8.8

**Verify on R1-Edge:**
show ip nat translations
show ip nat statistics
**Expected:** See PAT translations with inside local/global addresses

---

## WAN Connectivity

**From Branch PC (10.20.0.x):**
ping 10.10.50.10          (HQ Server)
ping 10.10.10.10          (HQ Sales PC)
tracert 8.8.8.8

**Verify routing on Branch-R2:**
show ip route
ping 10.10.50.10

---

## Port Security Testing

**On Access-SW3 (Finance ports):**
show port-security interface fa0/1
show port-security address

**Test violation:**
1. Connect PC to Finance port Fa0/1
2. Note MAC address learns
3. Disconnect and connect different PC
4. Port should shut down (if configured with `violation shutdown`)

---

## Performance Verification

### Bandwidth Test
Use Packet Tracer simulation mode:
1. Send ICMP packet from Sales to Engineering
2. Observe path: PC → Access-SW1 → Dist-SW1 → Core-1 → Dist-SW1 → Access-SW2 → PC
3. Verify no excessive hops or loops

### Spanning Tree
**On Dist-SW1:**
show spanning-tree vlan 10
**Expected:** Root bridge or designated port roles clear

---

## Troubleshooting Commands

### Connectivity Issues
show ip interface brief          (Check interface status)
show vlan brief                  (Verify VLAN assignment)
show interfaces trunk            (Check trunking)
show ip route                    (Verify routing table)
show arp                         (Check ARP cache)

### DHCP Issues
show ip dhcp binding             (Active leases)
show ip dhcp pool                (Pool statistics)
show ip dhcp conflict            (Address conflicts)

### NAT Issues
show ip nat translations         (Active translations)
show ip nat statistics           (NAT counters)
debug ip nat                     (Real-time NAT events)

---

## Documentation Sign-Off

| Test Category        | Status | Tester | Date |
|----------------------|--------|--------|------|
| Layer 2 (VLANs)      | ☐ Pass | ______ | ____ |
| Layer 3 (Routing)    | ☐ Pass | ______ | ____ |
| DHCP                 | ☐ Pass | ______ | ____ |
| Security (ACLs)      | ☐ Pass | ______ | ____ |
| NAT/Internet         | ☐ Pass | ______ | ____ |
| WAN Connectivity     | ☐ Pass | ______ | ____ |
| Port Security        | ☐ Pass | ______ | ____ |

**Network Engineer:** _________________________  
**Date:** ___________  
**Signature:** _____________________