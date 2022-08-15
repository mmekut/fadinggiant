##################################################
# Generated on phansible.com
# Curated by Mmekut
##################################################

Vagrant.configure("2") do |config|

    config.vm.define "Alma" do |c|
        # Unfortunately CentOS has been decapitated by RedHat
        # Almalinux becomes an alternative
        c.vm.provider :virtualbox do |v|
            v.name = "AlmaBox"
            v.customize [
                "modifyvm", :id,
                "--name", "AlmaBox",
                "--memory", 1024,
                "--cpus", 1,
                #"--cpu-profile", "host",
                "--natdnshostresolver1", "on"
            ]
        end
        
        # Will download box from vagrant cloud...
        #...if it hasn't been downloaded manually
        c.vm.box = "almalinux/8"
        
        # Sets VM boot timeouts
        # Vagrant will timeout if VM takes longer than this value to
        # complete booting but you can still ssh into the machine after a while
        c.vm.boot_timeout = 600
    
        c.vm.network :private_network, ip: "192.168.33.99"
        c.ssh.forward_agent = true

        
        #Installs ansible locally and provisions inside the VM
        c.vm.provision "ansible_local" do |ansible|
            # playbook n requirement details
            ansible.playbook = "ansible/playbook.yml"
            ansible.galaxy_role_file = 'ansible/requirements.yml'
           
            ansible.galaxy_roles_path = '/vagrant/ansible/roles'

            # Galaxy command installs collections n roles
            ansible.galaxy_command = "sudo ansible-galaxy install -r %{role_file}"
            # ansible 2.12 says collection n roles in one file can be installed with..
            # ..ansible-galaxy install -r %{role_file}

            # collection installation style from github.com/hashicorp/vagrant/issues/10958
            # sudo ansible-galaxy collection install -r %{role_file} && sudo ansible-galaxy install -r %{role_file} -p %{roles_path}
        end
        
        # Comment out before/during provisioning to avoid mount errors when booting VM --- only mounts when Apache is installed
        # Permission issues dealt with me for --- 4-months
        c.vm.synced_folder "www", "/var/www/fading",
        owner: "vagrant", group: "apache", mount_options: ["dmode=770", "fmode=750"]
    end
end