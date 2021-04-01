
# Answer
1. login to `net-exam-1`
```
	$ssh user@net-exam-1
```

2. enable ip forwarding
```
	$sudo sysctl -w net.ipv4.ip_forward=1
```

3. add iptables rule to redirect traffic to destination port
```
	$sudo iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 22022
```

4. make changes persistant
```
	$sudo iptables-save > /etc/sysconfig/iptables
```
