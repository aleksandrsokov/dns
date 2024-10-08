# DNS
Стенд 4 ВМ
ns01 - 192.168.50.10 master  
ns01 - 192.168.50.11 slave  
client - 192.168.50.15  
client2 - 192.168.50.16  


Настроен DNS сервер с зонами:  
dns.lab  
ddns.lab  
newdns.lab  

Так же настроен Split-DNS  

client  
доступны: www.newdns.lab и web1.dns.lab  
не доступны: web2.dns.lab

client2  
видит всю зону dns.lab и не видит зону newdns.lab
