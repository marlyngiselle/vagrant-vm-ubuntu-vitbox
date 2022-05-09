Vagrant.configure("2") do |config|

servidor_ip = "192.168.56.20"
box_os = "generic/ubuntu2004"
servidor_nombre_os =  "ubuntu"
vm_nombre_virtual_box = "ubuntu"
mi_llave_privada = "~/.ssh/id_ed25519"
mi_llave_publica = "~/.ssh/id_ed25519.pub"
llave_de_vagrant = "~/.vagrant.d/insecure_private_key"
ruta_servidor_authorized_keys = "/home/vagrant/.ssh/authorized_keys"
cantidad_ram = 1024
cantidad_cpu = 1

  # Deshabilita la insercion automatica de una key por parte de Vagrant
  config.ssh.insert_key = false

  # Llave privada: Configuramos 2 llaves posibles para usar como conexion, la de vcamacho y la de vagrant 
  config.ssh.private_key_path = [ mi_llave_privada , llave_de_vagrant ]

  # Llave publica - La guardamos en el authorized_keys del servidor para poder acceder por ssh con PubKeyAuthentication
  config.vm.provision "file", source: mi_llave_publica, destination: ruta_servidor_authorized_keys

  # La IP. OJO cuando se usa Host-Only Networking en VirtualBox, el rango permitido es unicamente 192.168.56.0/21 
  config.vm.network "private_network", ip: servidor_ip

  config.vm.synced_folder '.', '/vagrant', disabled: true

  # El sistema operativo, CPU y RAM
  config.vm.box = box_os
  config.vm.hostname = servidor_nombre_os
  config.vm.box_check_update = true
  config.vm.boot_timeout = 600
  config.vm.provider "virtualbox" do |vb|
    vb.name = vm_nombre_virtual_box
    vb.memory = cantidad_ram
    vb.cpus = cantidad_cpu
    vb.gui = true
    vb.check_guest_additions = false
    # vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end

  # El bootstrap si queremos ejecutar una especie de script inicial, ej: como el userdata de EC2
  # config.vm.provision "shell", path: "comandos.sh"

  # Mensaje para el usuario para cuando acabe el vagrant up, le diga que debe hacer despues para conectarse
  config.vm.post_up_message = "VAGRANT HA FINALIZADO CORRECTAMENTE! La VM esta lista y ahora puedes ingresar con usuario=vagrant y password=vagrant"
end
