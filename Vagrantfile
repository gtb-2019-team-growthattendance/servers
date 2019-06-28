Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder ".", "/vagrant",disabled: true
  config.ssh.insert_key = false

  config.vm.define "api001" do |users001|
    users001.vm.network "private_network", ip: "192.168.33.10"
  end

  config.vm.define "api002" do |users002|
    users002.vm.network "private_network", ip: "192.168.33.11"
    config.vm.provision "ansible" do |ansible|
       ansible.playbook = "ansible/role/api/api.yaml"
       ansible.inventory_path = "ansible/hosts"
       ansible.limit = "users"
    end
  end

  config.vm.define "lb001" do |webproxy002|
    webproxy002.vm.network "private_network", ip: "192.168.33.21"
    config.vm.provision "ansible" do |ansible|
       ansible.playbook = "ansible/role/lb/lb.yaml"
       ansible.inventory_path = "ansible/hosts"
       ansible.limit = "web-proxy"
    end
  end
end
