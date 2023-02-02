Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "web1" do |web1|
    web1.vm.box = "ubuntu/bionic64"
    web1.vm.network "private_network", ip: "192.168.56.16"
    web1.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = 2 
    end
    web1.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install apache2 wget unzip -y
    systemctl start apache2
    systemctl enable apache2
    cd /tmp/
    wget https://www.tooplate.com/zip-templates/2108_dashboard.zip
    unzip -o 2108_dashboard.zip
    cp -r 2108_dashboard/* /var/www/html/
    systemctl restart httpd
    SHELL
  end

  config.vm.define "db" do |db|
    db.vm.box = "geerlingguy/centos7"
    db.vm.network "private_network", ip: "192.168.56.17"
    db.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = 2
    end
  db.vm.provision "shell", inline: <<-SHELL
  yum install mariadb-server -y
  systemctl start mariadb
  systemctl enable mariadb


  mysql -u root -e "CREATE DATABASE wordpress;"
  mysql -u root -e "GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON wordpress.* TO wordpress@localhost;"
  mysql -u root -e "FLUSH PRIVILEGES;"
  
  SHELL
  
  end

end