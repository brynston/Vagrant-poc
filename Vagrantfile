

Vagrant.configure('2') do |config|
  config.vm.define "master-box" do |vb1|
    vb1.vm.box = 'ubuntu-14.04'
    vb1.vm.box_url = 'http://opscode-vm-bento.s3.amazonaws.com/'\
      "vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"

    vb1.vm.synced_folder '.', '/vagrant', id: 'vagrant-root'

    vb1.vm.provider "virtualbox" do |vb1|
      vb1.gui = true
      vb1.memory = 2048
      vb1.cpus = 4
      vb1.name = "ubuntu-docker-master"
      vb1.customize ["modifyvm", :id, "--vram", "64"]
    end
    
    config.vm.network "private_network", type: "dhcp"

    vb1.vm.provision 'shell', inline: 'apt-get install -y curl'
    vb1.vm.provision 'docker'
    vb1.vm.provision 'shell', inline: 'curl -SsL https://github.com/docker/compose/releases/download/1.5.0rc1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose'
    vb1.vm.provision 'shell', inline: 'chmod +x /usr/local/bin/docker-compose'
    vb1.vm.provision 'shell', inline: 'usermod -aG docker vagrant'

    # vb1.vm.provision 'shell', inline: 'sudo apt-get update'
    # vb1.vm.provision 'shell', inline: 'sudo apt-get install python-pip'
    # vb1.vm.provision 'shell', inline: 'sudo pip install ansible'
    # vb1.vm.provision 'shell', inline: 'sudo pip install paramiko PyYAML Jinja2 httplib2 six'
    # vb1.vm.provision 'shell', inline: 'sudo pip install markupsafe'
    # vb1.vm.provision 'shell', inline: 'echo "127.0.0.1" > ~ansible_hosts'
    # vb1.vm.provision 'shell', inline: 'export ANSIBLE_INVENTORY=~/ansible_hosts'
    # vb1.vm.provision 'shell', inline: 'ansible all -m ping --ask-pass'


  end

  config.vm.define "slave-box" do |vb2|
    vb2.vm.box = 'ubuntu-14.04'
    vb2.vm.box_url = 'http://opscode-vm-bento.s3.amazonaws.com/'\
      "vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"
    
    vb2.vm.synced_folder '.', '/vagrant', id: 'vagrant-root'

    vb2.vm.provider "virtualbox" do |vb2|
      vb2.gui = true
      vb2.memory = 2048
      vb2.cpus = 4
      vb2.name = "ubuntu-docker-slave"
      vb2.customize ["modifyvm", :id, "--vram", "64"]
    end

    config.vm.network "private_network", type: "dhcp"

    vb2.vm.provision 'shell', inline: 'apt-get install -y curl'
    vb2.vm.provision 'docker'
    vb2.vm.provision 'shell', inline: 'curl -SsL https://github.com/docker/compose/releases/download/1.5.0rc1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose'
    vb2.vm.provision 'shell', inline: 'chmod +x /usr/local/bin/docker-compose'
    vb2.vm.provision 'shell', inline: 'usermod -aG docker vagrant'
  end

end
