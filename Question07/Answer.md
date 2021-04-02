
# Answer

1. check if the container `FinanceFE` exists
```
	lxc-info --name FinanceFE
```
2. clone to the new container
```
	lxc-clone -P /srv/lxc FinanceFE testly
```
3. disable start on boot
```
	echo "lxc.start.auto = 0" >> /srv/lxc/testly/config
```
