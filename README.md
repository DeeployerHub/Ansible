## Local DNS server
* Linux [https://help.ubuntu.com/community/Dnsmasq](https://help.ubuntu.com/community/Dnsmasq)

* Mac 
```
brew install dnsmasq
echo 'address=/.deeployer.dev.com/192.168.200.200' > /usr/local/etc/dnsmasq.conf

sudo cp -fv /usr/local/opt/dnsmasq/*.plist /Library/LaunchDaemons
sudo chown root /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist
sudo launchctl load /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist
sudo launchctl stop homebrew.mxcl.dnsmasq
sudo mkdir -p /etc/resolver
sudo tee /etc/resolver/deeployer.dev.com > /dev/null <<EOF
nameserver nameserver 127.0.0.1
EOF

sudo launchctl start homebrew.mxcl.dnsmasq

dscacheutil -flushcache
```

## Create SSH key
```
ssh-keygen -t rsa -b 4096 -C "<your github email>"
```
## Copy your SSH key and paste it into your github account's ssh keys
```
cat ~/.ssh/id_rsa.pub | pbcopy
```

## Create the basic directories
```
mkdir ~/projects
mkdir ~/projects/waac
chmod -R 777 ~/projects
cd ~/projects/waac
```

## Clone the following repositories
```
git clone git@github.com:WAAC/Ansible.git ansible
git clone git@github.com:WAAC/d-web.git w-web
```

## Install Ansible & Vagrant
* Linux 
```
sudo apt-get install vagrant ansible virtualbox nfs-kernel-server
```
* Mac 
```
# make sure you installed virtual box before you start to head to this process
brew cask install vagrant
brew install ansible
```

## Start
```
cd ~/projects/waac/ansible
vagrant up
```
Use the following command incase you had problem with UID
```
id -u $(whoami) > .vagrant/machines/default/virtualbox/creator_uid
```
