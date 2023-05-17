# Devops-setup https://medium.com/@KuldipkumarPrajapati/vm-steps-5bbf8af414d0

1. get static IP
1. Create VM by choosing image, size, region and naming.
ssh to vm with root (ssh root@<server-ip>)
1. setup user accounts (adduser username)
1. add user to sudo group (usermod -aG sudo username)
1. setup public key authentication : create key (ssh-keygen -t rsa -b 4096 -c <email id>)
1. Adding SSH key to remote server: login with root and paste public key in (vim ~/.ssh/authorized_keys)
1. Disable password based auth in (/etc/ssh/sshd_config) replace with (PasswordAuthentication no)
1. Disable root login in (/etc/ssh/sshd_config) replace with (PermitRootLogin no)
1. Firewall (iptables): Command line program ufw (uncomplicated firewall) can be used to manage firewall(sudo ufw app list, sudo ufw allow openSSH)
1. Configure Time zone (sudo dpkg-reconfigure tzdata) with UTC in all server to avoid conflicts between servers. Install NTP (sudo apt install ntp) to keep in sync with global NTP server so when leap second get updated server update it as well.
1. Run App with PM2 : Install PM2 (yarn add pm2 — dev) and run nodejs app with pm2 start. Run npx pm2 startup to get script and run to restart pm2 if it crashes.
1. Disallow 8080 and allow 80: (sudo ufw allow 80, sudo ufw delete allow 8080)
1. Forward Traffic from 80 to 8080 port : (sudo iptables -t nat -I PREROUTING -p tcp — dport 80 -j REDIRECT — to-port 8080)
1. Configuring NGINX : update /etc/nginx/nginx.conf file as per need
1. DNS: Job of DNS is to resolve ip addresses. Computer first look to resolve ip in (/etc/hosts) file and then goes to resolving name server provided by ISP.
1. Zone file update: First buy domain and update zone file to resolve server IP address using Administrative UI. 
1. If you want to use Administrative UI of cloud, update custom DNS in Domain of Domain provider then you can use Route 53 of AWS and Admin UI for Digital Ocean.
1. A and AAAA records in Zone file: update A records (api IN A xxx.xx.xxx.xx)

# PM2 Commands
npx pm2 monit
pm2 show <id|name>
killing process: npx pm2 list, kill id
npx pm2 list