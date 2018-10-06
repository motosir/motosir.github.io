#### Headless VM


#### Setting up a new machine for ssh login
1) Get mac addres of new VM

```bash
VM="ubuntu-ud1"
VMFILE="/Users/$USER/Documents/Virtual Machines.localized/${VM}.vmwarevm/${VM}.vmx"
grep "ethernet0.generatedAddress =" "$VMFILE"
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
and restart service
```bash
sudo /Applications/VMware\ Fusion.app/Contents/Library/services/services.sh --stop
sudo /Applications/VMware\ Fusion.app/Contents/Library/services/services.sh --start
```

3) add entry in /etc/hosts
```shell
sudo echo "172.16.76.21  ud1" >> /etc/hosts
```

4) On the guest vm, restart vm  or 'sudo systemctl restart networking' to pick static IP form dhcp

5) copy public key to new vm
```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub user@host
```
or

```bash
HOST=ud1
RUSER=user
PUBKEY=$(cat ~/.ssh/id_rsa.pub)
ssh -t $RUSER@$HOST "[[ -d ~/.sshh ]] || { mkdir -p ~/.ssh; chmod 700 ~/.ssh; }; echo ${PUBKEY} >> ~/.ssh/authorized_keys; chmod 700 ~/.ssh/authorized_keys;"
```

6) add host entry to ssh config host
```bash
RUSER=user
echo -e "\n\nHost ud*\n   User $RUSER\n   IdentityFile ~/.ssh/id_rsa" >>  ~/.ssh/config
```

you should now be able ssh into vm by running
```bash
ssh ud1
```
