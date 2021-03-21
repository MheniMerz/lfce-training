
# Answer01
1. login to exam-1
```
	ssh username@exam-1
```
2. install rsyslog server
```
	sudo yum install rsyslog -y
```
3. edit the config file `/etc/rsyslog.conf` and uncomment the following lines (also change the port number to 9514)
```
	$ModLoad imudp
	$UDPServerRun 9514
```
4. if selinux is enforcing, allow the udp port 9514
```
	sudo semanage -a -t syslogd_port_t -p udp 9514
```
5. restart the service
```
	sudo systemctl restart rsyslog.service
```
6. make the service persistant (autostarts if the host reboots)
```
	sudo systemctl enable rsyslog.service
```
7. check if it's working properly
```
	sudo ss -unlp | grep 9514
```
