## 1. Check Listening Network Sockets and Processes

The ss command displays information about network sockets. It can be used to check listening ports and identify the processes using them.

```bash
sudo ss -tulpn
```

Options:

```text
-t  TCP sockets
-u  UDP sockets
-l  Listening sockets
-x  Unix domain sockets
-p  Process information
-n  Numeric addresses and ports
```

The -n option prevents ss from resolving port numbers and IP addresses into service names and hostnames. Remove -n if you want ss to perform name resolution:

```bash
sudo ss -tulp
```

Displays listening Unix domain sockets

```bash
sudo ss -xl
```
