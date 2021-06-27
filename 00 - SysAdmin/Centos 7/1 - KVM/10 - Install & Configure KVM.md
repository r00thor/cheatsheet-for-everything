# Install & Configure KVM
```bash
$ lscpu | grep Virtualization
Virtualization: VT-x
```

## 1. Install KVM
```
# yum install qemu-kvm libvirt libvirt-python libguestfs-tools virt-install kvm
```

```
# systemctl enable libvirtd  
# systemctl start libvirtd
```

## 2. Verify kvm installation
```
# lsmod | grep -i kvm
```

## 3. Configure bridged networking
```
# brctl show
bridge name     bridge id               STP enabled     interfaces
virbr0          8000.000000000000       yes
br0             8000.000e0cb30550       no              eth0
# virsh net-list
```
### Disable NetworkManager
```
# chkconfig NetworkManager off
# chkconfig network on
# service NetworkManager stop
# service network start
```
#### Creating network initscripts
```script
// Update your nic config file such as ifcfg-enp3s0 or em1
# vim /etc/sysconfig/network-scripts/ifcfg-enp3s0
// Add Line
BRIDGE=br0

// Save and close the file in vi. Edit /etc/sysconfig/network-scripts/ifcfg-br0 and add:
# vim /etc/sysconfig/network-scripts/ifcfg-br0
// Append the following:
DEVICE="br0"
# I am getting ip from DHCP server #
BOOTPROTO="dhcp"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
ONBOOT="yes"
TYPE="Bridge"
DELAY="0"
NM_CONTROLLED="no"

# service network restart
```
## 4. Configure iptables to allow all traffic to be forwarded across the bridge
```
// VIA IPTABLES
# iptables -I FORWARD -m physdev --physdev-is-bridged -j ACCEPT
# service iptables save
# service iptables restart
// VIA FIREWALL-CMD
# firewall-cmd --direct --add-rule ipv4 filter FORWARD 0 -m physdev --physdev-is-bridged -j ACCEPT
# firewall-cmd --reload
```

#### Prevent bridged traffic from being processed by iptables rules, this improves the bridge’s performance. In /etc/sysctl.conf append the following lines:
```bash
net.bridge.bridge-nf-call-ip6tables = 0
net.bridge.bridge-nf-call-iptables = 0
net.bridge.bridge-nf-call-arptables = 0
```
#### Reload the kernel parameters configured with sysctl:
```
# sysctl -p /etc/sysctl.conf
```
#### Restart the libvirt daemon:
```
# service libvirtd reload
```