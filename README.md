# Pacman repo for ALARM on Xiaomi Pad 5

## How to add

```bash
sudo pacman-key --recv-key 666411233117519B --keyserver keyserver.ubuntu.com
sudo pacman-key --lsign-key 666411233117519B
cat <<EOF | tee -a /etc/pacman.conf
[nabu-alarm]
SigLevel = Required DatabaseOptional
Server = https://nabu-alarm.github.io/repo
EOF
```
