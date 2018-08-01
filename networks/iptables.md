 # IPTABLES
 
 ## The Core Elementes of the IPTABLE System
 
 ```
 |-----------|         |-------------------|          |---------------------|              |-----------|
 |           |-------->|     PREROUTING    |--------->|        INPUT        |------------->|           |
 |           |         |-------------------|          |---------------------|              |           |
 |           |                         |                                                   |           |
 |           |                         |                                                   |           |
 |           |                         V                                                   |           |
 | network   |                  |------------|                                             | local     |
 | interface |                  |   FORWARD  |                                             | process   |
 |           |                  |------------|                                             |           |
 |           |                          |                                                  |           |
 |           |                          |                                                  |           |
 |           |                          V                                                  |           |
 |           |         |-------------------|          |---------------------|              |           |
 |           |<--------|    POSTROUTING    |<---------|       Output        |<-------------|           |
 |-----------|         |-------------------|          |---------------------|              |-----------|
 
 with:
 PREROUTING:  raw -> start of tracking -> mangle -> nat
 INPUT:       mangle -> filter
 FORWARD:     mangle -> filter
 OUTPUT:      raw -> start of tracking -> mangle -> nat -> filter
 POSTROUTING: mangle -> nat
 ```
 
 
 
 ### Tables
 
 | Tablename  | Description                                                         |
 |------------|---------------------------------------------------------------------|
 | `filter`   | Default table. Used for packet filtering.                           |
 | `mangle`   | Rules to change packet headers.                                     |
 | `nat`      | Routing rules for NAT networks.                                     |
 | `raw`      | Allows to apply rules before the kernel starts tracking the packet. |
 | `security` | Used to implement SELinux security policies.                        |
 
 ### Chains
 
 | Chainname     | Tables                 | Description                                                                         |
 |---------------|------------------------|-------------------------------------------------------------------------------------|
 | `PREROUTING`  | `mangle`, `nat`, `raw` |  Rules within this Chain are applied as the packets arrive on the network interface. |
 | `INPUT`       | `filter`, `mangle`     |  Rules within this Chain are applied just before the packets are handed over to local processes. |
 | `OUTPUT`      | `filter`, `mangle`, `nat`, `raw` | Rules within this Chain are applied just after a local process crafted packets. |
 | `FORWARD`     | `filter`, `mangle`     | Rules within this Chain are appplied to packets which are routed through the current host. |
 | `POSTROUTING` | `mangle`, `nat`        | Rules within this Chain are applied to packets just before they leave the network interface. |
 
 ### Targets
