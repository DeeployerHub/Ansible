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


        config.vm.synced_folder "~/projects/DeeployerHub", "/home/vagrant/projects/DeeployerHub-nfs", type: "nfs",  mount_options: ['rw', 'vers=3', 'tcp', 'actimeo=2']
        config.bindfs.bind_folder "/home/vagrant/projects/DeeployerHub-nfs", "/home/vagrant/projects/DeeployerHub"
    end

    config.vm.network "private_network", ip: "192.168.200.200"

    config.vm.network "forwarded_port", guest: 27017, host: 27017
    config.vm.network "forwarded_port", guest: 6379, host: 63799
    
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/dev.yml"
        ansible.verbose = "v"
    end

    config.vm.provider :lxc do |lxc|
        lxc.customize 'cgroup.memory.limit_in_bytes', '1024M'
    end
end

