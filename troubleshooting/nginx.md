## 1. Blocking IP on NGINX

Create the file blockip.conf at the following directory

```text
/etc/nginx/conf.d/blockip.conf
```

Add the IP adresses to block on the file

```text
# deny      IP
deny 192.168.0.1
```
