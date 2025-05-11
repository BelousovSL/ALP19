ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'
Vagrant.configure("2") do |config|
    config.vm.define "inetrrouter" do |inetrrouter|
        inetrrouter.vm.box = 'bento/ubuntu-24.04'
        inetrrouter.vm.host_name = 'inetrrouter'
        inetrrouter.vm.network :forwarded_port, host: 2301, guest: 22        
        inetrrouter.vm.network :private_network, ip: "192.168.255.1", netmask: "255.255.255.252", virtualbox__intnet: 'router-net', adapter: 2
        inetrrouter.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024    
        end        
        inetrrouter.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_inetrrouter/provision.yml"
            ansible.inventory_path = "ansible_inetrrouter/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "centralrouter" do |centralrouter|
        centralrouter.vm.box = 'bento/ubuntu-24.04'
        centralrouter.vm.host_name = 'centralrouter'
        centralrouter.vm.network :forwarded_port, host: 2302, guest: 22
        centralrouter.vm.network :private_network, ip: "192.168.255.2", netmask: "255.255.255.252", virtualbox__intnet: 'router-net', adapter: 2
        centralrouter.vm.network :private_network, ip: "192.168.0.1", netmask: "255.255.255.240", virtualbox__intnet: 'dir-net', adapter: 3
        centralrouter.vm.network :private_network, ip: "192.168.0.33", netmask: "255.255.255.240", virtualbox__intnet: 'hw-net', adapter: 4
        centralrouter.vm.network :private_network, ip: "192.168.0.65", netmask: "255.255.255.192", virtualbox__intnet: 'mgt-net', adapter: 5
        centralrouter.vm.network :private_network, ip: "192.168.255.9", netmask: "255.255.255.252", virtualbox__intnet: 'office1-central', adapter: 6
        centralrouter.vm.network :private_network, ip: "192.168.255.5", netmask: "255.255.255.252", virtualbox__intnet: 'office2-central', adapter: 7
        centralrouter.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024            
        end

        centralrouter.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_centralrouter/provision.yml"
            ansible.inventory_path = "ansible_centralrouter/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "centralserver" do |centralserver|
        centralserver.vm.box = 'bento/ubuntu-24.04'
        centralserver.vm.host_name = 'centralserver'
        centralserver.vm.network :forwarded_port, host: 2303, guest: 22
        centralserver.vm.network :private_network, ip: "192.168.0.2", netmask: "255.255.255.240", virtualbox__intnet: 'dir-net', adapter: 2        
        centralserver.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024            
        end

        centralserver.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_centralserver/provision.yml"
            ansible.inventory_path = "ansible_centralserver/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "office1router" do |office1router|
        office1router.vm.box = 'bento/ubuntu-24.04'
        office1router.vm.host_name = 'office1router'
        office1router.vm.network :forwarded_port, host: 2304, guest: 22
        office1router.vm.network :private_network, ip: "192.168.255.10", netmask: "255.255.255.252", virtualbox__intnet: 'office1-central', adapter: 2
        office1router.vm.network :private_network, ip: "192.168.2.1", netmask: "255.255.255.192", virtualbox__intnet: 'dev1-net', adapter: 3
        office1router.vm.network :private_network, ip: "192.168.2.65", netmask: "255.255.255.192", virtualbox__intnet: 'test1-net', adapter: 4
        office1router.vm.network :private_network, ip: "192.168.2.129", netmask: "255.255.255.192", virtualbox__intnet: 'managers-net', adapter: 5
        office1router.vm.network :private_network, ip: "192.168.2.193", netmask: "255.255.255.192", virtualbox__intnet: 'office1-net', adapter: 6        
        office1router.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024            
        end

        office1router.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_office1router/provision.yml"
            ansible.inventory_path = "ansible_office1router/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "office2router" do |office2router|
        office2router.vm.box = 'bento/ubuntu-24.04'
        office2router.vm.host_name = 'office2router'
        office2router.vm.network :forwarded_port, host: 2305, guest: 22
        office2router.vm.network :private_network, ip: "192.168.255.6", netmask: "255.255.255.252", virtualbox__intnet: 'office2-central', adapter: 2
        office2router.vm.network :private_network, ip: "192.168.1.1", netmask: "255.255.255.128", virtualbox__intnet: 'dev2-net', adapter: 3
        office2router.vm.network :private_network, ip: "192.168.1.129", netmask: "255.255.255.192", virtualbox__intnet: 'test2-net', adapter: 4
                office2router.vm.network :private_network, ip: "192.168.1.193", netmask: "255.255.255.192", virtualbox__intnet: 'office2-net', adapter: 5     
        office2router.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024            
        end

        office2router.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_office2router/provision.yml"
            ansible.inventory_path = "ansible_office2router/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "office1server" do |office1server|
        office1server.vm.box = 'bento/ubuntu-24.04'
        office1server.vm.host_name = 'office1server'
        office1server.vm.network :forwarded_port, host: 2306, guest: 22
        office1server.vm.network :private_network, ip: "192.168.2.130", netmask: "255.255.255.192", virtualbox__intnet: 'managers-net', adapter: 2
        office1server.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024            
        end

        office1server.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_office1server/provision.yml"
            ansible.inventory_path = "ansible_office1server/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end

    config.vm.define "office2server" do |office2server|
        office2server.vm.box = 'bento/ubuntu-24.04'
        office2server.vm.host_name = 'office2server'
        office2server.vm.network :forwarded_port, host: 2307, guest: 22
        office2server.vm.network :private_network, ip: "192.168.1.2", netmask: "255.255.255.128", virtualbox__intnet: 'dev2-net', adapter: 2
        office2server.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
            vb.memory = 1024            
        end

        office2server.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible_office2server/provision.yml"
            ansible.inventory_path = "ansible_office2server/hosts"
            ansible.host_key_checking = "false"
            ansible.limit = "all"
        end
    end
end