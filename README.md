# ansible-ara-poc Vagrant demo

 This is Vagrant testing playground for [Openstack ARA][1] 
 
It contains one machine with Ansible Openstack ARA named `ara` and 
two machines `node1` and `node2` to play with. 
 
## How to use:

 * Checkout `git clone --recursive https://github.com/VerosK/vagrant-ara-poc ara-poc`
 * Enter the `ara-poc` directory

 * Start machines by `vagrant up`
 * Open http://192.168.49.50:8080/ 

 * or run some ansible playbooks from `ara` host.
  
   
[1]: https://github.com/openstack/ara
