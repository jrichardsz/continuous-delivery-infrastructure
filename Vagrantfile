Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
  end
  config.vm.boot_timeout = 1000
  config.hostmanager.manage_host = true
  config.vm.define :jenkins do |jenkins|
    jenkins.vm.network "private_network", ip: "192.168.50.92"
    jenkins.vm.hostname = "jenkins.denschu.de"
  end
  config.vm.define :nexus do |nexus|
    nexus.vm.network "private_network", ip: "192.168.50.93"
    nexus.vm.hostname = "nexus.denschu.de"
  end
  config.vm.define :registry do |registry|
    registry.vm.network "private_network", ip: "192.168.50.96"
    registry.vm.hostname = "docker.denschu.de"
    registry.vm.provision "file", source: "certs/docker.crt", destination: "/tmp/certs/domain.crt"
    registry.vm.provision "file", source: "certs/docker.key", destination: "/tmp/certs/domain.key"
    registry.vm.provision :shell, :inline => "cp /tmp/certs/domain.crt /etc/ssl/certs/domain.crt"
    registry.vm.provision :shell, :inline => "cp /tmp/certs/domain.key /etc/ssl/certs/domain.key"
  end
  config.vm.define :testserver do |testserver|
    testserver.vm.network "private_network", ip: "192.168.50.97"
    testserver.vm.hostname = "testserver.denschu.de"
  end
end
