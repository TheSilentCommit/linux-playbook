## 1. Update the system

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Installing NGINX

```bash
sudo apt install nginx -y
```

## 3. Starting and enabling NGINX

```bash
sudo systemctl enable nginx

sudo systemctl start nginx

systemctl status nginx
```

## 4. Installing MariaDB-server and MariaDB-client

```bash
sudo apt install mariadb-server mariadb-client -y
```

## 5. Starting and enabling MariaDB

```bash
sudo systemctl enable mariadb

sudo systemctl start mariadb

systemctl status mariadb

sudo mysql_secure_installation
```

Recommended answers:

| Prompt | Answer |
|--------|:------:|
| Switch to unix_socket authentication | Y |
| Change the root password | N |
| Remove anonymous users | Y |
| Disallow root login remotely | Y |
| Remove test database and access to it | Y |
| Reload privilege tables | Y |

## 6. Creating WordPress Database

```bash
sudo mysql
```

```sql
CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'WpuserPasswd123!';

GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';

FLUSH PRIVILEGES;

EXIT;
```

## 7. Installing PHP

```bash
sudo apt install -y php-fpm php-mysql php-cli php-curl php-gd php-xml php-mbstring php-zip php-intl php-imagick
```

## 8. Installing WordPress

```bash
wget https://wordpress.org/latest.tar.gz

sudo tar -xzf  latest.tar.gz -C /var/www
```

## 9. Permissions

```bash
sudo chown -R www-data:www-data /var/www/wordpress

sudo find /var/www/wordpress -type d -exec chmod 755 {} +

sudo find /var/www/wordpress -type f -exec chmod 644 {} +
```

## 10. NGINX configuration

```bash
sudo nano /etc/nginx/sites-available/wordpress

server {
    listen 80;
    server_name _;
    
    root /var/www/wordpress;
    index index,php index.html;
    
    access_log /var/log/nginx/wordpress_access.log;
    error_log /var/log/nginx/wordpress_error.log;
    
    location / {
        try_files $uri $uri/ /index.php?$args;
    }
    
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.4-fpm.sock;
    }
    
    location ~ /\.ht {
        deny all;
    }
}
```

## 11. Enable the site

```bash
sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/

sudo rm /etc/nginx/sites-enabled/default

sudo nginx -t

sudo systemctl reload nginx
```

## 12. WordPress configuration

Edit the WordPress configuration file:

```bash
cd /var/www/wordpress

sudo cp wp-config-sample.php wp-config.php

sudo nano wp-config.php
```

Update the database settings:

```php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wpuser');
define('DB_PASSWORD', 'WpuserPasswd123!');
define('DB_HOST', 'localhost');
```

## 13. Firewall setup

```bash
sudo ufw allow OpenSSH

sudo ufw allow 'Nginx Full'

sudo ufw enable
```

## 14. Complete the WordPress Installation

On your server localhost http://127.0.0.1 complete the installation wizard by entering:

- Site Title
- Administrator Username
- Administrator Password
- Administrator Email

## 15. Backup

```bash
tar -czvf site-$(date +%Y%m%d-%H%M).tar.gz /var/www/site
```

The result will be site-Ydm-HM.tar.gz

To extract it use this

```bash
tar -xzf site-Ydm-HM.tar.gz
```
