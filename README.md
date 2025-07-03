# Pacman repo for ALARM on Xiaomi Pad 6

## How to add

```bash
sudo pacman-key --recv-key 666411233117519B --keyserver keyserver.ubuntu.com
sudo pacman-key --lsign-key 666411233117519B
cat <<EOF | tee -a /etc/pacman.conf
[pipa-alarm]
SigLevel = Required DatabaseOptional
Server = https://timoxa0.github.io/pipa-alarm-repo
EOF
```
