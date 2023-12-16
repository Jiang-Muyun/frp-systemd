# Setup_Ubuntu

```bash
sudo apt update
sudo apt upgrade
sudo apt install htop git zsh openssh-server vim tmux progress curl
sudo apt install smartmontools nvme-cli zfsutils-linux
```

type $env:USERPROFILE\.ssh\id_rsa.pub | ssh -P1234 IP "cat >> .ssh/authorized_keys"

### oh-my-zsh and plugins
```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
python3 -c "import os;P=os.getenv('HOME')+'/.zshrc';f=open(P);L=list(f);f.close();O=open(P,'w');[O.write('plugins=(git zsh-autosuggestions zsh-syntax-highlighting)\n') if l.startswith('plugins=') else O.write(l) for l in L]"
```

### Anaconda
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh -b
./miniconda3/bin/conda init zsh
rm Miniconda3-latest-Linux-x86_64.sh
```

### Add or remove user
```bash
userdel -r USERNAME
sudo useradd -m -p $(openssl passwd -1 "USER_PASSWORD") -s /bin/zsh USERNAME
sudo usermod -aG sudo USERNAME
```

### frp server
```bash
sudo systemctl stop frps
wget https://github.com/fatedier/frp/releases/download/v0.52.3/frp_0.52.3_linux_amd64.tar.gz
tar xvf frp_0.52.3_linux_amd64.tar.gz
sudo cp frp_0.52.3_linux_amd64/frps /usr/bin/frps
rm frp_0.52.3_linux_amd64.tar.gz

sudo nano /etc/systemd/system/frps.service
sudo systemctl daemon-reload && sudo systemctl enable frps && sudo systemctl start frps && sudo service frps restart
sudo systemctl status frps
```

### frp client
```bash
sudo systemctl stop frpc
wget https://github.com/fatedier/frp/releases/download/v0.52.3/frp_0.52.3_linux_amd64.tar.gz
tar xvf frp_0.52.3_linux_amd64.tar.gz
sudo cp frp_0.52.3_linux_amd64/frpc /usr/bin/frpc
rm frp_0.52.3_linux_amd64.tar.gz

sudo nano /etc/systemd/system/frpc.service
sudo systemctl daemon-reload && sudo systemctl enable frpc && sudo systemctl start frpc && sudo service frpc restart
sudo systemctl status frpc
```
