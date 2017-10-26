#!/bin/bash
# install dan setting openvpn
yum -y install openvpn
wget -O /etc/openvpn/openvpn.tar "https://gitlab.com/presult77/autoscript/raw/master/openvpn-debian.tar"
cd /etc/openvpn/
tar xf openvpn.tar
wget -O /etc/openvpn/1194.conf "https://gitlab.com/presult77/autoscript/raw/master/tcp1194.conf"
wget -O /etc/iptables.up.rules "https://gitlab.com/presult77/autoscript/raw/master/iptables.up.rules"
sed -i '$ i\iptables-restore < /etc/iptables.up.rules' /etc/rc.local
sed -i '$ i\iptables-restore < /etc/iptables.up.rules' /etc/rc.d/rc.local
MYIP=`curl icanhazip.com`;
MYIP2="s/xxxxxxxxx/$MYIP/g";
sed -i $MYIP2 /etc/iptables.up.rules;
sed -i 's/venet0/eth0/g' /etc/iptables.up.rules
iptables-restore < /etc/iptables.up.rules
sysctl -w net.ipv4.ip_forward=1
sed -i 's/net.ipv4.ip_forward = 0/net.ipv4.ip_forward = 1/g' /etc/sysctl.conf
service openvpn restart
chkconfig openvpn on
cd

# configure openvpn client config
cd /etc/openvpn/
wget -O /etc/openvpn/1194-client.ovpn "https://gitlab.com/presult77/autoscript/raw/master/openvpn.conf"
host=$( hostname )
host2="s/xxxxxxxxx/$host/g";
sed -i $host2 /etc/openvpn/1194-client.ovpn;
cp 1194-client.ovpn /home/vps/public_html/
