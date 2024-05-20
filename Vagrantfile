Vagrant.configure("2") do |config|

  # Sistema operativo basado en ubuntu
  config.vm.box = "ubuntu/xenial64"

  # Red Privada con IP "192.168.50.55"
  config.vm.network "private_network", ip: "192.168.50.55"

  # Carpeta sincronizada
  config.vm.synced_folder ".", "/vagrant_data"


  config.vm.provision "shell", inline: <<-SHELL

    # Elevar privilegios a superusuario
    sudo -i

    # Actualizar los paquetes
    sudo apt-get update -y

    # Instalar PHP, MySQL
    sudo apt-get install php php-mysql

    sudo apt-get install -y mysql-server

    # Generamos el la base de datos y la tabla con los inserts
    echo 'CREATE DATABASE gestion_restautante;' >> /home/vagrant/datos_menu.sql
    echo 'USE gestion_restautante;' >> /home/vagrant/datos_menu.sql
    echo 'CREATE TABLE restaurante (idPlato INT AUTO_INCREMENT PRIMARY KEY, nombre VARCHAR(50), descripcion VARCHAR(50), precio INT, categoria VARCHAR(50);' >> /home/vagrant/datos_menu.sql

    # Sincornizamos la carpeta
    config.vm.synced_folder "./datos_menu.sql",
    "/home/vagrant/datos_menu.sql"

   SHELL
end
