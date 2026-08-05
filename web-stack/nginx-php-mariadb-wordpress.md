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


