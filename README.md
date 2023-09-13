# Registration and Deregistration Process using Free5gc and Ueransim

### Registration Process:
After successful installation of free5gc and ueransim to do registration following steps to be followed
1. ssh in free5gc and run web-console in one terminal and stop it using ctrl+c and in the same terminal.

Remember to do if the vm free5gc is restarted give
```
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo systemctl stop ufw
sudo iptables -I FORWARD 1 -j ACCEPT
```
2. Run free5gc

```
cd ~/free5gc
./run.sh
```
3.ssh into free5gc in another terminal and give tcpdump
```
sudo tcpdump -i enp0s8 -w filename.pcap
```
4. start UERANSIM in another terminal and give
```
cd ~/UERANSIM
build/nr-gnb -c config/free5gc-gnb.yaml
```
5.start UERANSIM in another terminal and give
```
cd ~/UERANSIM
sudo build/nr-ue -c config/free5gc-ue.yaml  
```
Now stop the UE, GNB and tcpdump in order by using ctrl+c in the respective terminals. And now transfer the file from vm to your computer and check the generated packets in pcap file using wireshark.


### Deregistration Process:

1. shh into free5gc in 3 individual terminals.
•	Webconsole
•	To run free5gc
•	tcpdump

2. ssh into UERANSIM in 3 individual terminals.
•	GNB
•	UE
•	Deregistration

3. 1 ssh in free5gc and run web-console in one terminal.

Remember to do if the vm free5gc is restarted give
```
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
sudo systemctl stop ufw
sudo iptables -I FORWARD 1 -j ACCEPT
```
3.2 Run free5gc in another terminal.
```
cd ~/free5gc
./run.sh
```
3.3 ssh into free5gc in another terminal and give tcpdump
```
sudo tcpdump -i enp0s8 -w filename.pcap
```
3.4  start UERANSIM in another terminal for GNB and give
```
cd ~/UERANSIM
build/nr-gnb -c config/free5gc-gnb.yaml
```
3.5 start UERANSIM in another terminal for UE and give
```
cd ~/UERANSIM
sudo build/nr-ue -c config/free5gc-ue.yaml  
```
3.6 start the UERANSIM in another terminal for deregistration and give
```
cd ~/UERANSIM
build/nr-cli imsi-(xxxxxxxxxxxxxxx) --exec 'deregister normal'
```
  (or)

```
build/nr-cli imsi-(xxxxxxxxxxxxxxx)
```
note: imsi number is reflected on webconsole and the same to be used here

and give
```
commands
```
list of commands will appear give deregister and you will find
$deregister <normal|disable-5g|switch-off|remove-sim>
and give
```
deregister normal
```
Now stop the UE, GNB and tcpdump in order by using ctrl+c in the respective terminals. And now transfer the file from vm to your computer and check the generated packets in pcap file using wireshark.
