boxes = [
    {
        :name     => "vm1",
        :ip => "172.19.0.2",
        :ports    => [3301, 8181, 8183, 8185],
    },
    {
        :name     => "vm2",
        :ip => "172.19.0.3",
        :ports    => [],
    },
]

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end

  config.vm.box = "centos/7"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  boxes.each_with_index do |box, index|
    config.vm.define box[:name] do |box_config|
      box_config.vm.hostname = box[:hostname]
      box_config.vm.network "private_network", ip: box[:ip]
      box[:ports].each do |port|
        box_config.vm.network "forwarded_port",
                              guest: port,
                              host: port,
                              autocorrect: true
      end
    end
  end
end
