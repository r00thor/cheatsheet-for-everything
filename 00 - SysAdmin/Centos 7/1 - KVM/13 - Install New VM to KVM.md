# Install New VM to KVM
## Import Existent VM from QEMU
```bash 
# virt-install --import --name <VMName> --os-type linux --os-variant <you can search by $(osinfo-query os) command> --memory 2048 --vcpus 2 --cpu host --disk path=<target-vm-path>,format=qcow2,bus=virtio --network bridge=br0,model=virtio --graphics spice,listen=127.0.0.1 --noautoconsole
```

## From ISO install new VM

### Example Windows 10 Install:
```bash 
# virt-install --virt-type=kvm --name <VMName> --os-type windows --os-variant <you can search by $(osinfo-query os) command> --memory 4096 --vcpus 2 --cpu host --cdrom=<target-iso-path> --disk path=<target-vm-path>,size=40,bus=ide,format=qcow2 --network bridge=br0,model=virtio --graphics spice,listen=127.0.0.1 --noautoconsole
```

### Example Windows 10 Install:
```bash 
# virt-install --virt-type=kvm --name Windows-10 --os-type windows --os-variant win10 --memory 4096 --vcpus 2 --cpu host --cdrom=/var/lib/libvirt/isos/sysadmin/Win10_21H1_Spanish_x64.iso --disk path=/var/lib/libvirt/images/windows10.qcow,size=40,bus=ide,format=qcow2 --network bridge=br0,model=virtio --graphics spice,listen=127.0.0.1 --noautoconsole
```