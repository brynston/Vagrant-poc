

Vagrant.configure('2') do |config|
  config.vm.define "master-box" do |vb|
    vb.vm.box = 'ubuntu-14.04'
    vb.vm.box_url = 'http://opscode-vm-bento.s3.amazonaws.com/'\
      "vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"

    vb.vm.synced_folder '.', '/vagrant', id: 'vagrant-root'

    vb.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 8192
      vb.cpus = 4
      vb.name = "ubuntu-docker-master"
      vb.customize ["modifyvm", :id, "--vram", "64"]
    end

    vb.vm.provision 'shell', inline: 'apt-get install -y curl'
    vb.vm.provision 'docker'
    vb.vm.provision 'shell', inline: 'curl -SsL https://github.com/docker/compose/releases/download/1.5.0rc1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose'
    vb.vm.provision 'shell', inline: 'chmod +x /usr/local/bin/docker-compose'
    vb.vm.provision 'shell', inline: 'usermod -aG docker vagrant'
  end

  config.vm.define "slave-box" do |vb|
    vb.vm.box = 'ubuntu-14.04'
    vb.vm.box_url = 'http://opscode-vm-bento.s3.amazonaws.com/'\
      "vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"
    
    vb.vm.synced_folder '.', '/vagrant', id: 'vagrant-root'

    vb.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = 8192
      vb.cpus = 4
      vb.name = "ubuntu-docker-slave"
      vb.customize ["modifyvm", :id, "--vram", "64"]
    end

    vb.vm.provision 'shell', inline: 'apt-get install -y curl'
    vb.vm.provision 'docker'
    vb.vm.provision 'shell', inline: 'curl -SsL https://github.com/docker/compose/releases/download/1.5.0rc1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose'
    vb.vm.provision 'shell', inline: 'chmod +x /usr/local/bin/docker-compose'
    vb.vm.provision 'shell', inline: 'usermod -aG docker vagrant'
  end

end
