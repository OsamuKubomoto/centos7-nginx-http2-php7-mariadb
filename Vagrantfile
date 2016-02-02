Vagrant.configure(2) do |config|
  config.vm.define :dev do | dev |
    dev.vm.box = "bento/centos-7.2"
    dev.vm.hostname = "dev"
    dev.vm.network "private_network", ip: "192.168.33.10"
    dev.vm.network :private_network, ip: "192.168.0.1", virtualbox__intnet: "intnet"
    dev.vm.synced_folder ".", "/var/www/html", mount_options: ['dmode=777','fmode=755']
    dev.vm.provider :virtualbox do |v|
      v.customize ['modifyvm', :id, '--paravirtprovider', 'kvm']
    end
  end

  config.vm.define :ansible do | ansible |
    ansible.vm.box = "bento/centos-7.2"
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network", ip: "192.168.33.20"
    ansible.vm.network :private_network, ip: "192.168.0.2", virtualbox__intnet: "intnet"
    ansible.vm.synced_folder "./provision", "/home/vagrant/provision", mount_options: ['dmode=777','fmode=644']
    ansible.vm.provider :virtualbox do |v|
      v.customize ['modifyvm', :id, '--paravirtprovider', 'kvm']
    end
  end
end
