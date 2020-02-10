# -*- mode: ruby -*-
# vi: set ft=ruby :

# Based on Marcos Pereira's vagrant-java

Vagrant.configure("2") do |config|

  [8].each do |java_version|

    config.vm.define "java#{java_version}" do |vh|
      vh.vm.box = "ubuntu/bionic64"

      # Because I use these VMs when testing play stuff
      vh.vm.network "forwarded_port", guest: 9000, host: (9190 + java_version)

      vh.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
      end

      vh.vm.provision "shell", inline: <<-SHELL
        apt-get update
        apt-get install -y vim git git-core lynx unzip htop zip 
        # Install sbt
        apt-get install bc # see https://github.com/sbt/sbt/issues/3697
        echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
        apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
        apt-get update
        apt-get install sbt
        # Install Sdkman and java
        curl -s "https://get.sdkman.io" | bash
	source "/home/vagrant/.sdkman/bin/sdkman-init.sh"
	sdk install java 8.0.242.hs-adpt
      SHELL
    end

    config.vm.synced_folder "~/git/github/", "/host/git/github"

  end

end
