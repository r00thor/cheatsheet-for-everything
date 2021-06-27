# Useful commands

Let us see some useful commands for managing VMs.

#### List all VMs
`# virsh list --all `

#### Get VM info
`# virsh dominfo vmName`
`# virsh dominfo centos7-vm1`

#### Stop/shutdown a VM
`# virsh shutdown centos7-vm1`

#### Start VM
`# virsh start centos7-vm1`

#### Mark VM for autostart at boot time
`# virsh autostart centos7-vm1`

#### Reboot (soft & safe reboot) VM
`# virsh reboot centos7-vm1`  

#### Reset (hard reset/not safe) VM  
`# virsh reset centos7-vm1`

### Delete VM
`# virsh shutdown centos7-vm1`  
`# virsh undefine centos7-vm1`  
`# virsh pool-destroy centos7-vm1`
`# D=/var/lib/libvirt/images`
`# VM=centos7-vm1`
`# rm -ri $D/$VM`  

#### To see a complete list of virsh command type 
`# virsh help | less`
`# virsh help | grep reboot`