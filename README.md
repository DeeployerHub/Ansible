# Start
** Create SSH key
```
ssh-keygen -t rsa -b 4096 -C "<your github email>"
```
** Copy your SSH key and paste it into your github account's ssh keys
```
cat ~/.ssh/id_rsa.pub | pbcopy
```

* Create the basic directories
```
mkdir ~/projects
mkdir ~/projects/waac
chmod -R 777 ~/projects
cd ~/projects/waac
```

* clone the following repositories
```
git clone git@github.com:WAAC/Ansible.git ansible
git clone git@github.com:WAAC/d-web.git w-web
```
