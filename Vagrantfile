Vagrant.configure('2') do |config|
  
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.manage_guest = true
  config.hostmanager.ignore_private_ip = false
  
  config.ssh.insert_key = false

  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |v|
    v.cpus = 1
  end


  {
    'lb01'    => { ip: '192.168.135.101', mem: '256' },
    'app01'   => { ip: '192.168.135.111', mem: '256' },
    'app02'   => { ip: '192.168.135.112', mem: '256' },
    'db01'    => { ip: '192.168.135.121', mem: '512' },
  }.each do |short_name, vm_config|
    config.vm.define short_name do |host|
      host.vm.network 'private_network', ip: vm_config[:ip]
      host.vm.hostname = "#{short_name}"
      
      host.vm.provider "virtualbox" do |vb|
        vb.memory = vm_config[:mem]
      end
      
      # Copy the user's key to the vagrant's SSH keys and the authorized keys
      config.vm.provision "shell" do |s|
        ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
        s.inline = <<-SHELL
          echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
          echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
        SHELL
      end      
  
    end
  end
end