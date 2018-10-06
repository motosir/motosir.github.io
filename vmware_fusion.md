#### Headless VM


#### Adding a new Machine
1) Get mac addres of new VM

```bash
VM="ubunut-ud1"
VMFILE="/Users/$USER/Documents/Virtual Machines.localized/${VM}.vmwarevm/${VM}.vmx"
grep "ethernet0.generatedAddress"  $VMFILE
-
ethernet0.generatedAddress = "00:0C:29:BA:FE:D1"
```

2) create a static IP entry in
```bash
sudo vim /Library/Preferences/VMware\ Fusion/vmnet8/dhcpd.cfg
```
for the new vm guest
```shell
host ubuntu-ud1 { 
    hardware ethernet 00:0C:29:BA:FE:D1; 
    fixed-address 172.16.76.21;
}
```

