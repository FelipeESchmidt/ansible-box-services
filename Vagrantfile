$ip = "192.168.60.58"

$message = <<MSG
------------------------------------------------------

Box up in, #{$ip}
Accessible in http://#{$ip}

You can find more details in the link below
https://github.com/FelipeESchmidt/ansible-box-services

------------------------------------------------------
MSG

Vagrant.configure("2") do |config|

  config.vm.define "server" do |server|
    server.vm.box = "ubuntu/bionic64"
    server.vm.network "private_network", ip: $ip

    server.vm.provider "virtualbox" do |virtualboxMachine|
      virtualboxMachine.name = "FinalExam"
    end
  end

  config.vm.provision :"shell", path: "installPython.sh"
  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "./inventory"
    ansible.limit = "all"
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
  end

  config.vm.post_up_message = $message

end
