# Grafana

## HTTPS
установить сертбот
запустить `certbot --nginx`
заполнить там всё

закрыть порт 3000
```
iptables -A INPUT -p tcp -s 127.0.0.1 --dport 3000 -j ACCEPT

iptable -A INPUT -p tcp --dport 3000 -j DROP
```

# Create 1 DATASOURCE