### Quick start for frp

### Download frp
- from https://github.com/fatedier/frp/releases
```bash
wget https://github.com/fatedier/frp/releases/download/v0.49.0/frp_0.49.0_linux_amd64.tar.gz
tar -xvzf frp_0.49.0_linux_amd64.tar.gz
rm frp_0.49.0_linux_amd64.tar.gz
sudo mkdir /usr/local/frp
sudo cp frp_0.49.0_linux_amd64/frpc /usr/local/frp/
sudo cp frp_0.49.0_linux_amd64/frps /usr/local/frp/
```

### Server
- Modify `frps.ini`
  - YOUR_SECRET_STRING: password, any string
```bash
sudo cp frps.ini /usr/local/frp/
sudo cp frps.service /etc/systemd/system/frps.service
sudo systemctl daemon-reload && sudo systemctl enable frps && sudo systemctl start frps && sudo service frps restart
sudo service frps status
```

### Client
- Modify `frpc.ini`
  - Fill in YOUR_SERVER_IP: The IP or domain name of the relay server
  - YOUR_SECRET_STRING: password, any string
  - Add your needed ports

```bash
sudo cp frpc.ini /usr/local/frp/
sudo cp frpc.service /etc/systemd/system/frpc.service
sudo systemctl daemon-reload && sudo systemctl enable frpc && sudo systemctl start frpc && sudo service frpc restart
sudo service frpc status
```