
#Loadblancing 
#Ansible with Vagrant

#1, make home directory and clone code
mkdir /home/vagrant/ 
git clone https://github.com/quyetnguyen0989/vagrant-ansible

remembers & review : 
#2, files: 
nano bootstrap-mgmt.sh
copy examples into /home/vagrant (from inside the mgmt node)
cp -a /vagrant/examples/* /home/vagrant
chown -R vagrant:vagrant /home/vagrant
 
nano Vagrantfile


#3, Let's building

vagrant up
vagrant ssh mgmt

## Ping check 
 df -h
 ping web1
 ping web2
 ping lb
 ping web3
 ping web4
 ping web6

 
## Try ssh(remember type no)
 ssh web1
 ansible web1 -m ping
 
## Gen key ssh
ssh-keyscan web1
.ssh-keyscan lb web1 web2 >> .ssh/known_hosts
.cat .ssh/known_hosts
.ansible all -m ping --ask-pass
ansible all -m ping
ssh-keygen -t rsa -b 2048  
ssh-keyscan web3 web4 web5 web6 >> .ssh/known_hosts
ansible-playbook e45-ssh-addkey.yml --ask-pass
ansible all -m ping
ansible web1 -m setup -a "filter=ansible_hostname"
ansible web1 -m setup -a "filter=ansible_eth1"
ansible all -m shell -a "ifconfig"
 
# play play book load-balancing.
ansible-playbook e46-site.yml
