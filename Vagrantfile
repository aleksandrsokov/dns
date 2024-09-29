MACHINES = {
  :ns01 => {
        :box_name => "rockylinux/9",
        :vm_name => "ns01",
        #:public => {:ip => "10.10.10.1", :adapter => 1},
        :net => [   
                    #ip, adpter, netmask, virtualbox__intnet
                    ['192.168.50.10', 2, "255.255.255.0", "dns"],
                ]
  },

  :ns02 => {
        :box_name => "rockylinux/9",
        :vm_name => "ns02",
        :net => [
                    ['192.168.50.11', 2, "255.255.255.0", "dns"],
                ]
  },

  :client => {
        :box_name => "rockylinux/9",
        :vm_name => "client",
        :net => [
                    ['192.168.50.15', 2, "255.255.255.0", "dns"],
                ]
  },

  :client2 => {
        :box_name => "rockylinux/9",
        :vm_name => "client2",
        :net => [
                    ['192.168.50.16', 2, "255.255.255.0", "dns"],
                ]
  },

}

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      
      box.vm.provider "virtualbox" do |v|
        v.memory = 1500
        v.cpus = 2
       end

      boxconfig[:net].each do |ipconf|
        box.vm.network("private_network", ip: ipconf[0], adapter: ipconf[1], netmask: ipconf[2], virtualbox__intnet: ipconf[3])
      end

      if boxconfig.key?(:public)
        box.vm.network "public_network", boxconfig[:public]
      end

#      box.vm.provision "shell", inline: <<-SHELL
#        mkdir -p ~root/.ssh
#        cp ~vagrant/.ssh/auth* ~root/.ssh
#        systemctl restart sshd
#      SHELL

      if boxconfig[:vm_name] == "client2"
        box.vm.provision "ansible" do |ansible|
         ansible.playbook = "ansible/playbook.yml"
         #ansible.inventory_path = "ansible/hosts"
         #ansible.host_key_checking = "false"
         ansible.limit = "all"
        end
       end

    end
  end
end