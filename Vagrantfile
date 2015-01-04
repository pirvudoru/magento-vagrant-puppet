# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.host_name = "magento2"
  config.vm.define "magento2"

  config.vm.provision "shell", inline: "sudo apt-get install puppet -y"
  config.vm.synced_folder '.', '/vagrant', :disabled => true
  
  # Set the timezone
  config.vm.provision :shell, :inline => "echo \"EST\" |
    sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

  config.vm.provider :digital_ocean do |provider, override|
    override.ssh.private_key_path = 'C:\Users\Doru\.ssh\id_rsa'
    override.vm.box = 'digital_ocean'
    override.vm.box_url = "https://github.com/smdahlen/vagrant-digitalocean/raw/master/box/digital_ocean.box"

    provider.token = 'b6e6bfbfe2a07acfdde1d11e41dc2bca91ae310099292938fe961eedbc1b202a'
    provider.image = 'ubuntu-14-10-x64'
    provider.region = 'lon1'
    provider.size = '1gb'
    provider.ssh_key_name = 'Vagrant'
  end

  # PUPPET CONFIGS

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest file
  # in the manifests_path directory.
  config.vm.provision :puppet do |puppet|
  #  puppet.pp_path = "/tmp/vagrant-puppet"
    puppet.manifests_path = "puppet/manifests"
    puppet.manifest_file  = "base.pp"
    puppet.module_path    = "puppet/modules"
    puppet.options = "--verbose --debug"
  end
end
