
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Add the box version
  config.vm.box = "ubuntu_saucy_64_x86"
  config.vm.box_url = "http://glazzies.net/ubuntu_saucy_64_x86.box"

  # Config Web Server
  config.vm.define "web", primary: true do |web|
    # Run vm on lan and set mac address
    # web.vm.network "public_network", :bridge => 'eth0', :mac => "5CA1AB1E0001"
    config.vm.network :private_network, ip: "192.168.44.10"
    web.vm.network :forwarded_port, guest: 80, host: 8888

    web.vm.host_name = "web01.local"
    web.vm.provision :puppet do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "webserver.pp"
      puppet.module_path = "modules"
    end
    # config.vm.synced_folder "./www/", "/var/www/", :owner => "www-data"
    web.vm.provider "virtualbox" do |v|
     v.memory = 1024
    end

  end

  # config for the mysql db server box
  config.vm.define "db" do |db|
    # config.vm.network "public_network", :bridge => 'eth0', :mac => "5CA1AB1E0002"
    config.vm.network :private_network, ip: "192.168.44.11"
    db.vm.host_name = "db01.local"
    db.vm.provision :puppet do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "dbserver.pp"
      puppet.module_path = "modules"
    end
    db.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end

  # config for the mongodb server box
  config.vm.define "mongo" do |mongo|
    # config.vm.network "public_network", :bridge => 'eth0', :mac => "5CA1AB1E0003"
    mongo.vm.network :private_network, ip: "192.168.44.12"
    mongo.vm.host_name = "mongo.local"
    mongo.vm.provision :puppet do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "mongodb.pp"
      puppet.module_path = "modules"
    end
    mongo.vm.provider "virtualbox" do |v|
      v.memory = 1024
    end
  end
end
