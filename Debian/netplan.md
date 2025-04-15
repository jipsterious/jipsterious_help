# Netplan for dummy (me)

Using networkd service in the background.

## Home Network Config
Netplan iterates network configuration in sorting order.

eno1.yaml-
```
network:
  version: 2
  renderer: networkd
  ethernets:
    eno1:
      dhcp4: true
      dhcp4-overrides:
        route-metric: 50
```
bond1.yaml-
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp6s0f2: {}
    enp6s0f3: {}
  bonds:
    bond1:
      dhcp4: yes
      interfaces:
        - enp6s0f2
        - enp6s0f3
      parameters:
        mode: 802.3ad
        lacp-rate: fast
        mii-monitor-interval: 100
```
vlan.yaml-
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp6s0f1: {}
  vlans:
    vlan40:
      id: 40
      link: enp6s0f1
      dhcp4: yes
      dhcp4-overrides:
        route-metric: 150
        use-routes: no
      dhcp6: no
```
## Things I still need to figure out.
1. Bridge LXC network to host network.
2. Setup VLAN for bond network.
