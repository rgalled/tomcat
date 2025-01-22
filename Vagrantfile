Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.ssh.insert_key = false
  config.vm.define "tomcat" do |c|
    c.vm.hostname = "tomcat"
    c.vm.network "private_network", ip: "192.168.57.10"
    c.vm.network "forwarded_port", guest: 8080, host: 8080
    c.vm.provision "shell", inline: <<-SHELL
      apt update
      apt upgrade
      apt install -y git
      apt install -y openjdk-11-jdk
      apt install -y tomcat9
      apt install -y tomcat9-admin
      apt-get -y install maven
      mvn archetype:generate -DgroupId=org.zaidinvergeles -DartifactId=tomcat-war -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
      apt-get -y install maven
      mkdir /proyecto-piedra-papel-tijera
      groupadd tomcat9
      useradd -s /bin/false -g tomcat9 -d /etc/tomcat9 tomcat9
      cp /vagrant/local/tomcat-users.xml /etc/tomcat9/tomcat-users.xml
      cp /vagrant/local/context.xml /usr/share/tomcat9-admin/host-manager/META-INF/context.xml
      cp /vagrant/local/settings.xml /etc/maven/settings.xml 
      cp /vagrant/local/pom.xml /tomcat-war/pom.xml
      systemctl restart tomcat9
      systemctl start tomcat9
    SHELL
  end 
end
