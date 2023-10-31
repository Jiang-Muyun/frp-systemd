sudo nano /etc/systemd/system/frpc2.service
```
[Unit]
Description=frp client
Wants=network-online.target
After=network.target network-online.target

[Service]
ExecStart=/usr/local/frp/frpc -c /usr/local/frp/frpc.ini

[Install]
WantedBy=multi-user.target
```

sudo nano /usr/local/frp/frpc.ini
```
[common]
server_addr = XXXXXX
server_port = XXXXXX
token = XXXXXX
tls_enable = true

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = XXXXXX
```

```
sudo systemctl daemon-reload
sudo systemctl enable frpc 
sudo systemctl start frpc
sudo service frpc restart
sudo service frpc status
```
