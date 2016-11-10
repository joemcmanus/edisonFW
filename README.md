# edisonFW
A basic firewall config for the Intel Edison (Poky)
--------------

This contains two files, a systemd startup file and a sample iptables config allowing SSH, HTTP and HTTPS. 

Copy iptables.service in to /lib/systemd/system/. 

    cp iptables.service  /lib/systemd/system/.

Then copy the config file in to /etc/iptables.save 

    cp iptables.save /etc/. 

Next enable the service 

    systemctl enable iptables.service

Start the service

   systemctl start ipables.service 

Verify the rules

   iptables -L -n 

    Chain INPUT (policy ACCEPT)
    target     prot opt source               destination         
    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0            state RELATED,ESTABLISHED
    ACCEPT     icmp --  0.0.0.0/0            0.0.0.0/0           
    ACCEPT     all  --  0.0.0.0/0            0.0.0.0/0           
    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            state NEW tcp dpt:22
    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            state NEW tcp dpt:80
    ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            state NEW tcp dpt:443
    REJECT     all  --  0.0.0.0/0            0.0.0.0/0            reject-with icmp-host-prohibited
    
    Chain FORWARD (policy ACCEPT)
    target     prot opt source               destination         
    REJECT     all  --  0.0.0.0/0            0.0.0.0/0            reject-with icmp-host-prohibited
    
    Chain OUTPUT (policy ACCEPT)
    target     prot opt source               destination         
    root@edison1:/lib/systemd/system# 


