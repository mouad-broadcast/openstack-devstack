# openstack-devstack 
# Openstack {Bobcat} release
## Install openstack with devstack on ubuntu 22.04 
```
git clone https://opendev.org/openstack/devstack -b stable/2023.2
cd devstack/tools
sudo ./create-stack-user.sh
cd ../..
sudo mv devstack /opt/stack
sudo chown -R stack.stack /opt/stack/devstack
touch /opt/stack/devstack/local.conf
sudo su - stack
cd /opt/stack/devstack
./stack.sh
```
## To use openstack cmd
```
source /opt/stack/devstack/openrc admin admin
```

## FIX OCTAVIA loadbalancer problems after rebbot
```
vi /etc/systemd/system/devstack@o-da.service

PermissionsStartOnly=true
ExecStartPre=-/bin/mkdir -p /run/octavia
ExecStartPre=/bin/chown stack:root /run/octavia
ExecStartPre=/bin/chmod -R 755 /run/octavia

systemctl daemon-reload
```
## FIX bridges configurations after reboot
```
sudo ip addr flush dev br-ex
sudo ip addr add 172.24.4.1/24 dev br-ex
sudo ip link set br-ex up
ip route add  10.0.0.0/24 via 172.24.4.1
```
