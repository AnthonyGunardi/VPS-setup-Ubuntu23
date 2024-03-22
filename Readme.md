# VPS Setup - Ubuntu 23


## Get root access
---
- Check the current user
```
whoami
```

- Set password for default root account
```
sudo passwd
```

- Create user
```
sudo adduser your_username
```

- Get root access for user
```
sudo usermod -aG root your_username
```

&nbsp;

## Install git
---
```
sudo apt install git -y
```

&nbsp;

## Fetch and sync the latest package lists from repository
---
```
sudo apt update
sudo apt upgrade
```

&nbsp;

## Install node.js
---
- Check the available version for the node.js package
```
sudo apt policy nodejs
```

- Install Node.js
```
sudo apt install nodejs
sudo apt install npm
```

- Alternative: Install Node.js 20
```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install nodejs
```

&nbsp;

## Install pm2
---
- Install process manager (pm2)
```
sudo npm install -g pm2
```

- Start application with pm2
```
pm2 start app.js --name AppName --wait-ready --listen-timeout 4000 --watch --ignore-watch="FolderName"
```

- Saving the application list to be restored at reboot
```
pm2 save
```

- Manually restore saved application list at reboot
```
pm2 resurrect
```

- Generate script to add pm2 into system startup of Ubuntu
```
pm2 startup
```

&nbsp;

## Install nginx
---
- Install nginx package
```
sudo apt install nginx
```

- Start nginx service
```
sudo systemctl start nginx
```

- Add nginx service to system startup of Ubuntu
```
sudo systemctl enable nginx
```

- Install nano text editor
```
sudo apt install nano
```

- Edit nginx config
```
sudo nano /etc/nginx/nginx.conf
```

- Check syntax of nginx config
```
sudo nginx -t
```

- Restart nginx service
```
sudo systemctl restart nginx
```

- Create SSL Certificate.crt from .pem file for nginx
```
cat your_domain_name_cert.pem CA_bundle.crt >> certificate.crt
```

- Tuning kernel parameter. Place [this file](https://github.com/AnthonyGunardi/Linux-kernel-config) into "/etc/sysctl.d/nginx-tuning.conf"
```
sudo sysctl -p /etc/sysctl.d/nginx-tuning.conf
```

&nbsp;

## Install MySQL
---
- Install MySQL package
```
sudo apt install mysql-server
```

- Start MySQL service
```
sudo systemctl start mysql
```

- Add MySQL service to system startup of Ubuntu
```
sudo systemctl enable mysql
```

- Set secure installation
```
sudo mysql_secure_installation
```

- Check if MySQL accept remote connection (bind-address = 0.0.0.0)
```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

- Login to MySQL shell (example: username: root)
```
mysql -u root -p
```

- Change password of default root account
```
ALTER USER 'root'@'localhost' IDENTIFIED with mysql_native_password;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
FLUSH PRIVILEGES;

```

- Create custom root account
```
CREATE USER 'your username'@'%' IDENTIFIED BY 'your password';
```

- Allow Remote Access to MySQL
```
GRANT ALL PRIVILEGES ON *.* TO 'your username'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

- Create new mySQL database (example: testdb)
```
CREATE DATABASE testdb
```
