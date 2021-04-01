
# Answer01
1. make a file listing the target hostnames 
```
	~$cat <<EOF>> target_hosts.txt
	WEBSRV1
	WEBSRV2
	EOF
```
2. add ssh fingerprint to the `known_hosts` file
```
	$ ssh-keyscan -f target_hosts.txt
```
3. run the `/usr/local/bin/configtool` script simultaneously using `pssh`, make sure to provide the password when asked
```
	pssh --inline --askpass --user=student -h target_hosts.txt /usr/local/bin/configtool
```
