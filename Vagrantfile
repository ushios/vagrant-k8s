VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.define "master" do |node|
    node.vm.box = "ubuntu16.04"
    node.vm.box_url = "https://atlas.hashicorp.com/bento/boxes/ubuntu-16.04/versions/2.3.0/providers/virtualbox.box"

    node.vm.network :private_network, ip: "192.168.100.10"
    node.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2210

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision/vagrant.yml"
      ansible.inventory_path = "provision/hosts"
      ansible.limit = 'all'
    end
  end
end
