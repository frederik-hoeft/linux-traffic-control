# linux-traffic-control

A collection of Linux `tc` related scripts to achieve various things

## Contents

### VLAN

Configures a physical and VLAN interface pair to operate in a Cisco-style access mode. Any ingress traffic on the physical interface is tagged and redirected to the VLAN interface, while egress traffic on the VLAN interface is stripped and forwarded to the physical interface. This allows VLAN unaware devices to participate in a VLAN network.

Assuming the following interfaces:

- `eth0`: Physical interface
- `eth0.100`: VLAN interface

The following commands will configure a VLAN interface to operate in access mode on VLAN100:

```bash
src/vlan/vlan-access-mode-up.sh -i eth0 -v 100
```

To tear down the interface:

```bash
src/vlan/vlan-access-mode-down.sh -i eth0 -v 100
```

Notes:

- The current implementation will replace any existing `tc` configuration on the specified interfaces. 
- IP and routing configuration must be done separately.
- `vlan-access-mode-up.sh` should be executed after both interfaces are up and `vlan-access-mode-down.sh` should be executed before either interface goes down.