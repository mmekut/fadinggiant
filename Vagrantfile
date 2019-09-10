##################################################
# Generated on phansible.com
# Curated by Mmekut
##################################################

Vagrant.configure("2") do |config|

    config.vm.define "centOS" do |c|
        
        c.vm.provider :virtualbox do |v|
            v.name = "centOS"
            v.customize [
                "modifyvm", :id,
                "--name", "centOS",
                "--memory", 1024,
                "--natdnshostresolver1", "on",
                "--cpus", 1,
            ]
        end
        
        # Will download box from vagrant cloud...
        #...if it hasn't been downloaded manually
        c.vm.box = "centos/7"
        
        # Sets VM boot timeouts
        # Vagrant will timeout if VM takes longer than this value to
        # complete booting but you can still ssh into the machine after a while
        c.vm.boot_timeout = 600
    
        c.vm.network :private_network, ip: "192.168.33.99"
        c.ssh.forward_agent = true

        
        #Installs ansible locally and provisions inside the VM
        c.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "ansible/playbook.yml"
            ansible.inventory_path = "ansible/inventories/dev"
            ansible.galaxy_role_file = 'ansible/requirements.yml'
           
            ansible.galaxy_roles_path = '/vagrant/ansible/roles'
            ansible.galaxy_command = 'sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path}'
        end
        
        #syncronized folders in host and guest
        c.vm.synced_folder "www", "/var/www/fading"
    end
end