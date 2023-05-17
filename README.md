# Devops-setup

get static IP
Create VM by choosing image, size, region and naming.
ssh to vm with root (ssh root@<server-ip>)
setup user accounts (adduser username)
add user to sudo group (usermod -aG sudo username)
setup public key authentication : create key (ssh-keygen -t rsa -b 4096 -c <email id>)
Adding SSH key to remote server: login with root and paste public key in (vim ~/.ssh/authorized_keys)
Disable password based auth in (/etc/ssh/sshd_config) replace with (PasswordAuthentication no)
Disable root login in (/etc/ssh/sshd_config) replace with (PermitRootLogin no)
Firewall (iptables): Command line program ufw (uncomplicated firewall) can be used to manage firewall(sudo ufw app list, sudo ufw allow openSSH)
Configure Time zone (sudo dpkg-reconfigure tzdata) with UTC in all server to avoid conflicts between servers. Install NTP (sudo apt install ntp) to keep in sync with global NTP server so when leap second get updated server update it as well.
Run App with PM2 : Install PM2 (yarn add pm2 — dev) and run nodejs app with pm2 start. Run npx pm2 startup to get script and run to restart pm2 if it crashes.
Disallow 8080 and allow 80: (sudo ufw allow 80, sudo ufw delete allow 8080)
Forward Traffic from 80 to 8080 port : (sudo iptables -t nat -I PREROUTING -p tcp — dport 80 -j REDIRECT — to-port 8080)
Configuring NGINX : update /etc/nginx/nginx.conf file as per need
DNS: Job of DNS is to resolve ip addresses. Computer first look to resolve ip in (/etc/hosts) file and then goes to resolving name server provided by ISP.
Zone file update: First buy domain and update zone file to resolve server IP address using Administrative UI. If you want to use Administrative UI of cloud, update custom DNS in Domain of Domain provider then you can use Route 53 of AWS and Admin UI for Digital Ocean.
A and AAAA records in Zone file: update A records (api IN A xxx.xx.xxx.xx)

# PM2 Commands
npx pm2 monit
pm2 show <id|name>
killing process: npx pm2 list, kill id
npx pm2 list