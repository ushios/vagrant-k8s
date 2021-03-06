VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.define "master01" do |node|
    node.vm.box = "ubuntu16.04"
    node.vm.box_url = "https://atlas.hashicorp.com/bento/boxes/ubuntu-16.04/versions/2.3.0/providers/virtualbox.box"

    node.vm.hostname = "master01"
    node.vm.network :private_network, ip: "192.168.100.10"
    node.vm.network :forwarded_port, guest: 22, host: 2210

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision/master01.yml"
      ansible.inventory_path = "provision/hosts"
      ansible.limit = 'all'
    end

    node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1512"]
    end
  end

  config.vm.define "worker01" do |node|
    node.vm.box = "ubuntu16.04"
    node.vm.box_url = "https://atlas.hashicorp.com/bento/boxes/ubuntu-16.04/versions/2.3.0/providers/virtualbox.box"

    node.vm.hostname = "worker01"
    node.vm.network :private_network, ip: "192.168.100.11"
    node.vm.network :forwarded_port, guest: 22, host: 2211

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision/worker01.yml"
      ansible.inventory_path = "provision/hosts"
      ansible.limit = 'all'
    end

    node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1512"]
    end
  end
end
