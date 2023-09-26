## PreInstall steps:
- run ```docker-install.sh```
- verify docker installation
- if running on raspberry pi os run ```sudo apt install linux-modules-extra-raspi```
- reboot system
- open port ```51820/udp``` on the router for the device in use
- add duckDNS subdomain

## Procedure for PiHole + Unbound + Wireguard as installed service. 
- sudo apt update && sudo apt upgrade -y
- curl -sSL https://install.pi-hole.net | bash
- sudo ufw allow 443 && sudo ufw allow 80
- link for 5min block
http://{IP_pihole}/admin/api.php?disable=300&auth=${ cat /etc/pihole/setupVars.conf |grep WEBPASSWORD}
- pihole webUI settings 1
    1. add list from firebog
    2. update gravity
- change rouiter setting/DNS
    1. first => pihole ipv4 and ipv6
    2. second => google ipv4 and ipv6
- install unbound
    1. sudo apt install unbound -y
    2. sudo vim /etc/unbound/unbound.conf.d/pi-hole.conf
        - add config from: https://docs.pi-hole.net/guides/dns/unbound/
- pihole webUI settings 2
    3. change settings/DNS  ipv4 = 127.0.0.1#5335 and allow all
- install wireguard 
    1. curl -L https://install.pivpn.io | bash
    2. change sudo vim /etc/sysctl.conf
        - uncomment ```net.ipv4.ip_forward=1```
    3. generate certificates

## Resilio and DuckDNS as docker containers
- edit .env
- docker compose up
