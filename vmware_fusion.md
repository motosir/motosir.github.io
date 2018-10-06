#### Headless VM


#### Adding a new Machine
1) Get mac addres of new VM
    XX:XX:XX:XX:XX:XX
    
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

