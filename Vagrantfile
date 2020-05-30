IMAGE_NAME = "bento/ubuntu-16.04"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

    config.vm.define "master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.0.10"
        master.vm.hostname = "master"
        #master.vm.provision "ansible" do |ansible|
         #   ansible.playbook = "/Users/mac/Desktop/kube-usign-ansible/master-playbook.yml"
          #  ansible.extra_vars = {
           #     node_ip: "192.168.0.10",
            #}
        #end
    end

    config.vm.define "HAProxy" do |loadbalancer|
        loadbalancer.vm.box = "centos/8"
        loadbalancer.vm.box_url = "centos/8"
        loadbalancer.vm.network "private_network", ip: "192.168.0.13"
        loadbalancer.vm.hostname = "HAProxy"

    end

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.0.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            #node.vm.provision "ansible" do |ansible|
             #   ansible.playbook = "/Users/mac/Desktop/kube-usign-ansible/node-playbook.yml"
              #  ansible.extra_vars = {
               #     node_ip: "192.168.0.#{i + 10}",
                #}
            #end
        end
    end
end



