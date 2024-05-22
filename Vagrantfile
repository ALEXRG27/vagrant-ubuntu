Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-22.04"
  config.vm.network "forwarded_port", guest: 80, host: 1337

  config.vm.define 'ubuntu' do |machine|
    machine.vm.network "private_network", ip: "172.17.177.12"
    machine.vm.provision :ansible_local do |ansible|
       ansible.playbook       = "setup_docker.yml"
       ansible.verbose        = true
       ansible.install        = true
       ansible.limit          = "all" # or only "nodes" group, etc.
       ansible.inventory_path = "inventory"
    end
  end
end