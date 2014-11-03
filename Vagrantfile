Vagrant.configure("2") do |config|
    config.vm.box = "trusty64"
    config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

    config.vbguest.auto_update = true    
    config.vm.hostname = "blog"
    config.hostsupdater.aliases = ["blog.vagrant", "www.blog.vagrant"]
    config.vm.synced_folder 'vagrant_shared', '/var/www/blog', :nfs => true

    config.ssh.forward_agent = true
    config.vm.network :private_network, ip: "192.168.50.101"

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/config/host_vagrant"
        ansible.extra_vars = "ansible/config/vagrant.json"
        ansible.host_key_checking = false
        #ansible.verbose = "v"
        ansible.limit = "all"
    end
end
