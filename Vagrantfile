Vagrant.configure(2) do |config|
    config.vm.provider "virtualbox" do |v|
	    v.name = "WAAC_Ansible"
        host = RbConfig::CONFIG['host_os']
        if host =~ /darwin/
            v.cpus = `sysctl -n hw.ncpu`.to_i
        elsif host =~ /linux/
            v.cpus = `nproc`.to_i
        end
        v.customize ["modifyvm", :id, "--memory", 512]
        config.vm.box = 'ubuntu/trusty64'
        config.vm.box_check_update = false

        config.vm.synced_folder "~/projects/waac", "/home/vagrant/projects/waac", owner: "vagrant", group: "vagrant"

        config.vm.provider "lxc" do |v, override|
            v.container_name = 'WAAC_Ansible'
            override.vm.box = 'fgrehm/trusty64-lxc'
            override.vm.box_url = 'https://vagrantcloud.com/fgrehm/trusty64-lxc'
            override.vm.synced_folder "~/projects/waac", "/home/vagrant/projects/waac", type: "nfs"
        end
    end

    config.vm.network "private_network", ip: "192.168.200.200", lxc__bridge_name: 'vlxcbr1'

    config.vm.network "forwarded_port", guest: 27017, host: 27017

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/dev.yml"
        ansible.verbose = "v"
    end
end

