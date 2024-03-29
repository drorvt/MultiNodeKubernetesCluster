IMAGE_NAME = "ubuntu/bionic64"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    # Virtualbox configuration
    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 1
    end
      
    # K8s master configuration
    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.51.10"
        master.vm.hostname = "k8s-master"

        # Virtualbox configuration
        master.vm.provider "virtualbox" do |v|
            v.cpus = 2
        end
    end

    # K8s worker configuration
    (1..N).each do |i|
        config.vm.define "k8s-node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.51.#{i + 10}"
            node.vm.hostname = "k8s-node-#{i}"
        end
    end

    config.vm.provision "ansible_local" do |ansible|
        ansible.config_file = "ansible.cfg"
        ansible.playbook = "playbook.yml"
        ansible.groups = {
            masters: ["k8s-master"],
            nodes: ["k8s-node-1","k8s-node-2", "k8s-node-3"]
        }
    end

end
