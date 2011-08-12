Vagrant::Config.run do |config|
  config.vm.define :db_master do |db1_config|
    db1_config.vm.box = "ubuntu-10.04.2"
    db1_config.vm.box_url = "http://c3338508.r8.cf0.rackcdn.com/ubuntu-10.04.2.box"

    db1_config.vm.forward_port("ssh",22,2022)

    db1_config.vm.customize do |vm|
      vm.memory_size = 200 
    end

    db1_config.vm.network("33.33.33.22")

    db1_config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = ["cookbooks"]
      chef.add_recipe('mysql::server')
      chef.json.merge!({
        :mysql => {
          :server_root_password => 'root',
          :bind_address =>'33.33.33.22',
          :server_id => '22',
          :master => true
        },
      })
    end
  end

  config.vm.define :db_slave do |db2_config|
    db2_config.vm.box = "ubuntu-10.04.2"
    db2_config.vm.box_url = "http://c3338508.r8.cf0.rackcdn.com/ubuntu-10.04.2.box"

    db2_config.vm.forward_port("ssh",22,2023)

    db2_config.vm.customize do |vm|
      vm.memory_size = 200 
    end

    db2_config.vm.network("33.33.33.23")

    db2_config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = ["cookbooks"]
      chef.add_recipe('mysql::server')
      chef.json.merge!({
        :mysql => {
          :server_root_password => 'root',
          :bind_address => '33.33.33.23',
          :server_id => '23',
          :slave => true
        },
      })
    end
  end

  config.vm.define :db_remote_slave do |db3_config|
    db3_config.vm.box = "ubuntu-10.04.2"
    db3_config.vm.box_url = "http://c3338508.r8.cf0.rackcdn.com/ubuntu-10.04.2.box"

    db3_config.vm.forward_port("ssh",22,2024)

    db3_config.vm.customize do |vm|
      vm.memory_size = 200 
    end

    db3_config.vm.network("44.44.44.24")

    db3_config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = ["cookbooks"]
      chef.add_recipe('mysql::server')
      chef.json.merge!({
        :mysql => {
          :server_root_password => 'root',
          :bind_address => '44.44.44.24',
          :server_id => '24',
          :slave => true
        }
      })
    end
  end

end
