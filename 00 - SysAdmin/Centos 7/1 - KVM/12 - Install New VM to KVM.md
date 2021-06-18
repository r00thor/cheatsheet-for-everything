# Install New VM to KVM

## Import Existent VM from QEMU
```bash 
# virt-install --import --name <VMName> --os-variant <you can search by $(osinfo-query os) command> --memory 2048 --vcpus 2 --cpu host --disk path=<target-vm-path>,format=qcow2,bus=virtio --network bridge=br0,model=virtio --graphics spice --noautoconsole
```