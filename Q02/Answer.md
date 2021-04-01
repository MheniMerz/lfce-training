
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
	# check what ports are allowed by selinux (usually default ports 514 for syslog)
	$ sudo semanage port -l | grep syslog
		syslog_tls_port_t              tcp      6514, 10514
		syslog_tls_port_t              udp      6514, 10514
		syslogd_port_t                 tcp      601, 20514
		syslogd_port_t                 udp      514, 601, 20514
	
	# add the new udp port to the list of allowed ports (make sure to match the type from the previous output)
	$ sudo semanage port --add --type syslogd_port_t --proto udp 9514
	
	# check that it has been successfully added
	$ sudo semanage port -l | grep syslog
		syslog_tls_port_t              tcp      6514, 10514
		syslog_tls_port_t              udp      6514, 10514
		syslogd_port_t                 tcp      601, 20514
		syslogd_port_t                 udp      9514, 514, 601, 20514
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
