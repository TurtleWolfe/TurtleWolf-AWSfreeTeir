## AWSfreeTEARz
`sudo passwd`  
`sudo apt update`  
`sudo apt upgrade -y`  
`sudo apt dist-upgrade -y`  
`sudo nano /etc/ssh/sshd_config`  
```
Port 22222 
Protocol 2 
AllowGroups admins sshusers sudo 
# AllowUsers ubuntu jane_doe 
PermitRootLogin no 
PasswordAuthentication no 
```
`sudo nano /etc/skel/.bashrc`  
```
Force Color Prompt
PS1 = ..
```
`sudo timedatectl set-timezone America/New_York`  
`sudo adduser jane_doe`  
`sudo usermod -aG sudo jane_doe`  
cp /home/ubuntu/.ssh/authorized_keys /home/jane_doe/.ssh/authorized_keys
`sudo apt install fail2ban`  
`sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`  
`sudo nano /etc/fail2ban/jail.local`  
```
ignoreip = 127.0.0.1/8 ::1 10.0.0.0/24 xx.xx.xx.xx/32
enabled = true 
port 22222
```
`sudo ufw allow proto tcp from xx.xx.xx.xx/32 to port 22222`
`sudo ufw enable`

`systemd-resolve --status |grep DNS\ Servers`
install apache & webmin  
## post-boot checklist
sudo su
passwd
exit
sudo passwd --lock root

sudo cat /etc/shadow
   14  ssh-keygen
   15  cd .ssh
   18  chmod 400 id_rsa
   20  chmod 400 id_rsa.pub
   21  ls -al
   22  nano id_rsa.pub
   23  nano authorized_keys
scp -i "id_rsa" AWS:.ssh/id_rsa .
eval $(ssh-agent)
ssh-add id_rsa
$ scp ~/.ssh/config AWS:.ssh/config
## Update, Upgrade, AutoRemove & dist-upgrade
sudo apt-get -y upgrade (eof 2)
sudo apt-get -y autoremove
sudo apt -y dist-upgrade (2 more eof's)


sudo systemctl status -l fail2ban
sudo fail2ban-client status

systemctl status ssh
sudo netstat -tulpn |grep ssh

ssh-keygen
chmod 400 id_rsa
chmod 400 id_rsa.pub


AllowUsers john@(your-ip) john@(other-ip)
```
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -m recent --update --seconds 60 --hitcount 4 --rttl --name SSH -j LOG --log-prefix "SSH_brute_force "
iptables -A INPUT -p tcp --dport 22 -m recent --update --seconds 60 --hitcount 4 --rttl --name SSH -j DROP
```
## install Apache
sudo apt-get install apache2 -y  

### PHP

    39  sudo add-apt-repository ppa:ondrej/php
    38  sudo apt-get install python-software-properties
    40  sudo apt-get install software-properties-common
    41  sudo add-apt-repository ppa:ondrej/php
    42  sudo apt update
    43  apt list --upgradable
    44  sudo apt install -y php7.2
    45  sudo apt install php7.2-curl php7.2-gd php7.2-json php7.2-mbstring php7.2-xml
    46  sudo apt install apache2 libapache2-mod-php7.2
    47  sudo apt install php7.2-mysql
    48  sudo apt install phpmyadmin
    49  sudo systemctl restart apache2.service
    50  sudo systemctl restart mysql.service
    51  sudo fail2ban-client status
    52  sudo systemctl status -l fail2ban
    53  sudo systemctl status -l apache2
    54  cd /var/www
    55  ls
    57  cd html
    58  ls
    59  touch index.php
    60  sudo touch index.php
    61  sudo nano index.php
    62  ls
    63  rm index.html
    64  sudo rm index.html
    65  ls
    66  rm index.php
    67  sudo rm index.php

## CodeIgniter
cd /var/www  
which apache2  
sudo wget https://github.com/bcit-ci/CodeIgniter/archive/3.1.9.zip   
sudo apt install unzip  
sudo unzip 3.1.9.zip  
sudo mv CodeIgniter-3.1.9 CodeIgniter  
sudo rm 3.1.9.zip  
cd CodeIgniter



    3  sudo systemctl status -l fail2ban
    4  sudo fail2ban-client status
    1  which apache2
    6  sudo apt-get install apache2 -y
   10  wget https://github.com/bcit-ci/CodeIgniter/archive/3.1.9.zip
   11  sudo wget https://github.com/bcit-ci/CodeIgniter/archive/3.1.9.zip
   14  sudo apt install unzip
   16  sudo unzip 3.1.9.zip
   18  sudo mv CodeIgniter-3.1.9 CodeIgniter
   20  sudo rm 3.1.9.zip
   21  cd CodeIgniter
   33  sudo systemctl status -l apache2

### Bonfire

    1  sudo apt update
    2  sudo apt upgrade
    3  sudo apt-get install lamp-server^
    4  sudo mysql
    mariadb -u root -p
MariaDB [(none)]>
```
CREATE DATABASE codeigniter;
GRANT ALL ON codeigniter.* TO 'appuser'@'localhost' IDENTIFIED BY 'Aa1!Aa1!';
SHOW DATABASES;
SELECT HOST, USER, authentication_string FROM mysql.user;
SHOW GRANTS FOR 'appuser'@'localhost';
USE codeigniter;
```

    5  sudo mysql_secure_installation
    //   sudo apt install phpmyadmin
    6  cd /var/www/html
    7  sudo git clone https://github.com/ci-bonfire/Bonfire.git
    8  sudo nano /var/www/html/Bonfire/application/config/config.php
```
$config['base_url']     = 'http:// and always put the trailing /';
```    
    9  sudo nano /var/www/html/Bonfire/application/config/database.php
```
    'hostname'     => '127.0.0.1',
    'username'     => 'appuser',
    'password'     => 'Aa1!Aa1!',
    'database'     => 'codeigniter',
    'dbdriver'     => 'mysqli',
    'dbprefix'     => 'bf_',
```
    10  sudo nano /etc/apache2/sites-available/000-default.conf
```
DocumentRoot /var/www/html/Bonfire/public
```    
sudo nano /var/www/html/Bonfire/application/config/autoload.php
```
$autoload['libraries'] = array('database', 'email', 'session');
```

    11  sudo service apache2 reload
    12  sudo reboot
    13  history

    14  ping mysql.cclyqephhrtn.us-east-1.rds.amazonaws.com
    15  telnet 10.0.16.22 3306

## Node
## Express
## React
   36  sudo apt-get install nodejs
   38  node -v
   42  npm -v
   43  sudo npm -v
   44  sudo apt install npm
   45  npm -v
   46  node
   54  npm init
   63  npm -v
   73  sudo apt-get install curl python-software-properties
   74  sudo apt-get install curl software-properties-common
   75  curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
   76  sudo apt-get install -y nodejs
   77  sudo npx create-react-app my-app
   81  sudo npm update
   83  sudo ufw allow proto tcp from 71.88.119.101 to any port 3000
   85  sudo reboot
   86  sudo ufw status
   89  cd my-app
   90  npm start
sudo ufw allow proto tcp from 71.88.119.101 to any port 3000
  106  cd my-app
  108  sudo npm i react-router-dom

## Nginx Installation
    5  wget http://nginx.org/keys/nginx_signing.key
    6  apt-key add nginx_signing.key
    7  sudo apt-key add nginx_signing.key
    8  nano /etc/apt/sources.list.d/nginx.list
    9  sudo nano /etc/apt/sources.list.d/nginx.list
    10  apt-get update
    11  sudo apt-get update
    12  apt-get install nginx
    13  sudo apt-get install nginx
    14  /usr/sbin/nginx -t
    15  sudo /usr/sbin/nginx -t
    41  sudo reboot
    71  nginx -V
```
deb http://nginx.org/packages/mainline/ubuntu/ bionic nginx
deb-src http://nginx.org/packages/mainline/ubuntu/ bionic nginx
```
    8  sudo mv favicon.ico /usr/share/nginx/html
    9  cd /usr/share/nginx/html
    16  sudo nano index.html
## Nginx Configuration   
## httPERF
    23  sudo apt install httperf  
    24  httperf 
httperf --server 54.174.64.249 --port 80 --uri /index.html --rate 1000 --num-conn 30000 --num-call 1 --timeout 1
```
httperf --timeout=1 --client=0/1 --server=54.174.64.249 --port=80 --uri=/index.html --rate=1000 --send-buffer=4096 --recv-buffer=16384 --num-conns=30000 --num-calls=1
httperf: warning: open file limit > FD_SETSIZE; limiting max. # of open files to FD_SETSIZE
Maximum connect burst length: 3

Total: connections 30000 requests 30000 replies 30000 test-duration 29.998 s

Connection rate: 1000.1 conn/s (1.0 ms/conn, <=47 concurrent connections)
Connection time [ms]: min 0.7 avg 3.9 max 46.3 median 1.5 stddev 6.6
Connection time [ms]: connect 1.9
Connection length [replies/conn]: 1.000

Request rate: 1000.1 req/s (1.0 ms/req)
Request size [B]: 76.0

Reply rate [replies/s]: min 999.7 avg 1000.0 max 1000.3 stddev 0.3 (5 samples)
Reply time [ms]: response 1.9 transfer 0.0
Reply size [B]: header 238.0 content 611.0 footer 0.0 (total 849.0)
Reply status: 1xx=0 2xx=30000 3xx=0 4xx=0 5xx=0

CPU time [s]: user 11.28 system 15.57 (user 37.6% system 51.9% total 89.5%)
Net I/O: 903.4 KB/s (7.4*10^6 bps)

Errors: total 0 client-timo 0 socket-timo 0 connrefused 0 connreset 0
Errors: fd-unavail 0 addrunavail 0 ftab-full 0 other 0
```
## autoBENCH
## openWebLoad
## Deploying a basic site
    56  cd /etc/nginx/conf.d
    59  nano default.conf
    60  sudo mkdir -p /var/www/vhosts
    75  sudo cp -a /usr/share/nginx/html/. /var/www/vhosts
    86  sudo nano default.conf
    87  nginx -s reload
    88  sudo nginx -s reload
    89  service nginx status
    91  systemctl reload nginx
    92  systemctl status nginx
    106  sudo chmod -R o+r /var/www/vhosts
    107  sudo chown -R nginx:nginx /var/www/vhosts
    108  systemctl reload nginx
    112  service nginx status
    114  cd /etc/nginx/conf.d
    118  sudo nano default.conf
    119  systemctl reload nginx
    124  cd /var/www/vhosts
    125  sudo nano index.html
    135  sudo nano /etc/nginx/conf.d/default.conf
    136  systemctl reload nginx
    137  sudo nano default.conf
    140  sudo nano /etc/nginx/conf.d/default.conf
    142  apt-get install python-pip
    143  sudo apt-get install python-pip
    144  pip install ngxtop
    145  ngxtop -l /var/log/nginx/access.log
    146  sudo ngxtop -l /var/log/nginx/access.log
    147  systemctl reload nginx
    148  sudo ngxtop -l /var/log/nginx/access.log
    149  sudo nano /etc/nginx/conf.d/default.conf
    150  sudo reboot
    151  pip install ngxtop
    158  sudo -H pip install ngxtop
    159  ngxtop -l /var/log/nginx/access.log
    160  sudo ngxtop -l /var/log/nginx/access.log
    162  sudo ngxtop -l /var/log/nginx/access.log.1
    164  sudo ngxtop -l /var/log/host.nginx/access.log
    167  sudo touch /var/log/nginx/host.access.log
    172  sudo nano /etc/nginx/conf.d/default.conf
    174  sudo systemctl reload nginx
    175  sudo ngxtop -l /var/log/nginx/host.access.log
## NginX reverse proxy Apache
  235  sudo systemctl restart nginx
  236  systemctl status nginx.service
  238  sudo service nginx status
  239  fg
  240  sudo nano default.conf
  241  sudo service nginx status
  242  sudo nano default.conf
  243  sudo service nginx status
  244  which fastcgi
  245  apt-get install php7.2-fpm
  246  sudo apt-get install php7.2-fpm
  250  cd /etc/nginx/
  251  cd conf.d
  254  ls
  255  sudo nano /etc/nginx/conf.d/default.conf
  256  cd /var/www/CodeIgniter
  260  sudo nano /etc/nginx/conf.d/default.conf
  265  apt list --upgradable -a
  266  sudo apt upgrade
  267  apt list --upgradable -a
  281  cat error.log
  282  sudo cat error.log
  290  sudo nano /etc/nginx/conf.d/default.conf
  291  sudo service nginx restart
  292  sudo service nginx status
  297  sudo cat /var/log/nginx/error.log
  301  cd /usr/bin/php
  304  aptitude install libxml2-dev libevent-dev
  305  sudo apt install aptitude
  307  sudo aptitude install libxml2-dev libevent-dev
  308  sudo apt-get purge `dpkg -l | grep php| awk '{print $2}' |tr "\n" " "`
  315  which php
  341  find / -name php-7.2.0.tar.gz
  342  sudo find / -name php-7.2.0.tar.gz
  362  wget https://www.php.net/distributions/php-7.2.19.tar.gz
  364  tar -xvf php-7.2.19.tar.gz