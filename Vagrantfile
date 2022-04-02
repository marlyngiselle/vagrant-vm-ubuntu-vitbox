Vagrant.configure("2") do |config|

  config.ssh.insert_key = false
  config.ssh.private_key_path = ["C:/Users/Giselle Da Costa/.ssh/id_rsa", "C:/Users/Giselle Da Costa/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "C:/Users/Giselle Da Costa/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/authorized_keys"

  config.vm.network "private_network", ip: "192.168.33.15"

  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = "ubuntu-server"
  config.vm.box_check_update = true

  config.vm.provider "virtualbox" do |vb|
    vb.name = "ubuntu-20-04"
    vb.memory = 2048
    vb.cpus = 2
    vb.gui = true
    vb.check_guest_additions = false
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update -y
    apt-get upgrade -y
    timedatectl set-timezone Europe/Paris

    usuario=giselle
    useradd -U $usuario -m -s /bin/bash -G sudo
    echo "$usuario:123" | chpasswd
    echo "$usuario ALL=(ALL) NOPASSWD: ALL" | tee -a /etc/sudoers

    sed -i /etc/sudoers -re 's/^%sudo.*/%sudo ALL=(ALL:ALL) NOPASSWD: ALL/g'
    sed -i 's/^PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
    sed -i 's/^#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config
    systemctl restart sshd
  SHELL

end
