# -*- mode: ruby -*-
# vi: set ft=ruby :
#
$ansible_mode = 'ansible'

VAGRANTFILE_API_VERSION = "2"

VIRTUAL_MACHINES = {
  :ara => {
    :ip             => '192.168.49.50',
    :memory         => 2048,
  },
  :node1 => {
    :ip             => '192.168.49.51',
    :memory         => 1024,
  },
  :node2 => {
    :ip             => '192.168.49.52',
    :memory         => 1024,
  },
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.hostmanager.enabled = true
  config.vm.box = "vStone/centos-7.x-puppet.3.x"
  config.vm.box_check_update = false

  config.ssh.insert_key = false

  VIRTUAL_MACHINES.each do |name,cfg|

    config.vm.define name do |vm_config|
      vm_config.vm.hostname = name
      vm_config.vm.network :private_network, ip: cfg[:ip]

      config.vm.provider :virtualbox do |vb|
        vb.memory = cfg[:memory]
        vb.cpus = 1
        vb.linked_clone = true

      end # provider

      config.vm.provision $ansible_mode do |ansible|
            ansible.playbook = "site.yml"
            ansible.sudo_user = 'root'
            ansible.sudo = true
            ansible.verbose = "v"

            if ENV['ANSIBLE_TAGS'] then ansible.tags = ENV['ANSIBLE_TAGS']; end

            ansible.groups = {
              'vagrant'   => VIRTUAL_MACHINES.keys,
           }
           #ansible.limit = 'all'
      end

      if name == :ara then
          config.vm.provision 'shell',
            name: 'run ansible',
            privileged: false,
            inline: 'cd /vagrant; ansible-playbook site.yml'
      end
    end
  end
end

