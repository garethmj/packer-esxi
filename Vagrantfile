# Vagrant.require_plugin "vagrant-esxi"


File.open("version.txt", 'w') do |f|
  f.write(Vagrant::VERSION)
end

Vagrant.configure("2") do |config|
  config.ssh.default.username = "root"
  config.ssh.shell = "sh"

  config.vm.hostname = "esxi"
  config.vm.synced_folder ".", "/vagrant", nfs: true

  [:vmware_workstation, :vmware_fusion].each do |name|
    config.vm.provider name do |v,override|
      
      config.vm.provision "shell", inline: "echo Using VMware provisioner"
      config.vm.box = "vmware_esxi55"
      config.vm.box_url = "./vmware_esxi55.box"
      v.gui = true
      v.vmx["memsize"] = "65536"
      v.vmx["numvcpus"] = "12"
      v.vmx["cpuid.coresPerSocket"] = "6"
    end
  end

  config.vm.provision "shell", privileged: false, path: "provision.sh"
  config.vm.provision "shell", inline: "echo Configuration complete"
end
