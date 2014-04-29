require 'yaml'

$docker_install_script = <<SCRIPT
wget -q -O - https://get.docker.io/gpg | apt-key add -
echo deb http://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list
apt-get update -qq
apt-get install -q -y --force-yes lxc-docker
usermod -a -G docker vagrant
su - vagrant -c 'echo alias d=docker >> ~/.bash_aliases'
SCRIPT

CONF = YAML.load_file('server_config.yml')

Vagrant.configure('2') do |config|
  config.vm.box = 'phusion/ubuntu-14.04-amd64'

  config.vm.network :forwarded_port, guest: 3000, host: 3000
  CONF['forward_ports'].each do |port|
    config.vm.network :forwarded_port, guest: port, host: port
  end

  config.vm.synced_folder '.', '/vagrant', type: 'nfs'
  config.vm.network :private_network, ip: CONF['private_ip']

  config.vm.provider :virtualbox do |provider, override|
    provider.customize ['modifyvm', :id, '--name',   CONF['name']]
    provider.customize ['modifyvm', :id, '--memory', CONF['memory']]
  end

  if Dir.glob("#{File.dirname(__FILE__)}/.vagrant/machines/default/*/id").empty?
    config.vm.provision :shell, :inline => $docker_install_script
  end
end