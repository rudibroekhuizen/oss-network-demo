# oss-network-demo

Try an open source software based network, using OPNsense and Cumulus. Depends on:
- https://github.com/naturalis/ansible-opnsense v1.3
- https://github.com/naturalis/ansible-cumulus v1.1

See requirements.yml in ansible/roles

### Install vagrant-vbguest plugin on host

    wget -c https://releases.hashicorp.com/vagrant/2.2.4/vagrant_2.2.4_x86_64.deb
    sudo dpkg -i vagrant_2.2.4_x86_64.deb
    vagrant plugin install vagrant-vbguest

### Run vagrant up on host
    # Download repo:
    git clone -b v0.4 https://github.com/naturalis/oss-network-demo/
   
    # Start switches:
    oss-network-demo/switches> vagrant up

    # Start firewalls:
    oss-network-demo/firewalls> vagrant up

    # Start workstations:
    oss-network-demo/workstations> vagrant up

### Install lxml and srm on oob-mgmt-server

    oss-network-demo/switches> vagrant ssh oob-mgmt-server
    sudo pip install lxml
    sudo pip3 install lxml
    sudo apt install secure-delete

### Download git repo on oob-mgmt-server and install Ansible roles
    oss-network-demo/switches> vagrant ssh oob-mgmt-server
    sudo -s
    su cumulus
    cd ~/
    git clone -b v0.4 https://github.com/naturalis/oss-network-demo/
    cd oss-network-demo/ansible/basic/roles
    ansible-galaxy install -r requirements.yml --roles-path .

### Run ansible commands from oob-mgmt-server
    cd oss-network-demo/ansible/basic
    
    # Test connectivity to firewalls and switches
    ansible -m command -a "uptime" firewalls
    ansible all -m shell -a 'uptime' -l firewalls
    ansible -m command -a "uptime" switches

    # Deploy switches:
    oss-network-demo/ansible/basic> ansible-playbook switches.yml

    # Deploy firewalls:
    oss-network-demo/ansible/basic> ansible-playbook firewalls.yml

### Login to webinterface firewalls from host
    Firewall1: https://localhost:10443
    Firewall2: https://localhost:2209
    Firewall3: https://localhost:2211

### Test
    mtr --tcp 172.16.1.1
    mtr --udp 172.16.1.1

### VirtualBox commands
    vboxmanage showvminfo 1552905337_firewall2
