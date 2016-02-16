Vagrant.configure(2) do |config|
    config.vm.provider "virtualbox" do |v|
        host = RbConfig::CONFIG['host_os']
        if host =~ /darwin/
            v.cpus = `sysctl -n hw.ncpu`.to_i
        elsif host =~ /linux/
            v.cpus = `nproc`.to_i
        end
        v.customize ["modifyvm", :id, "--memory", 1024]
        config.vm.box = 'ubuntu/trusty64'

        if host =~ /linux/
            config.vm.synced_folder "~/projects/waac", "/home/vagrant/projects/waac", type: "nfs"
        else
            config.vm.synced_folder "~/projects/waac", "/home/vagrant/projects/waac"
        end
    end

    config.vm.network "private_network", ip: "192.168.200.200"

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/dev.yml"
        ansible.verbose = "v"
    end
end
