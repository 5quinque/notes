# firewalld

## Reject traffic from IP Address

`firewall-cmd --permanent --add-rich-rule="rule family='ipv4' source address='192.168.0.11' reject"`