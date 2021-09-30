Vagrant.configure("2") do |config|

  config.vm.network :private_network,
    ip: '192.168.1.100',
    libvirt__network_name: 'De-ICE',
    libvirt__dhcp_enabled: false,
    libvirt__forward_mode: 'nat',
    libvirt__host_ip: '192.168.1.1',
    model_type: 'e1000',
    autostart: true

  config.vm.provider :libvirt do |libvirt|
    libvirt.storage :file, :device => :cdrom, :path => "#{Dir.pwd}/De-ICE_S1.100.iso"
    libvirt.boot 'cdrom'
    libvirt.mgmt_attach = false
  end

end
