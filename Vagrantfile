VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'hashicorp/precise64'

  json_config_path = File.join("test", "boxes.json")
  list = File.open(json_config_path).read
  list = JSON.parse(list)

  list.each do |vm|
    config.vm.define vm["name"] do |web|
      web.vm.network "forwarded_port", guest: 22, host: vm["port"]
      web.vm.provision "shell", inline: "apt-get update && apt-get install --yes acl csh"

      vm["users"].each do |user|
        web.vm.provision "shell", inline: "useradd --create-home #{user}"
      end
    end
  end
end
