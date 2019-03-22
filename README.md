# oss-network-demo

Try an open source software based network, using OPNsense and Cumulus.

### Update Ansible on oob-mgmt-server

```bash
vagrant ssh oob-mgmt-server

sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```


### Install vagrant-vbguest plugin
```bash
wget -c https://releases.hashicorp.com/vagrant/2.2.4/vagrant_2.2.4_x86_64.deb
sudo dpkg -i vagrant_2.2.4_x86_64.deb
vagrant plugin install vagrant-vbguest
```



