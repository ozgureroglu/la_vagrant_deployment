# -*- mode: ruby -*-
# vi: set ft=ruby :

# ---- Configuration variables ----

GUI               = false # Enable/Disable GUI
RAM               = 512   # Default memory size in MB
RAM2              = 1024


# Network configuration
DOMAIN            = ".liderahenk.org"
NETWORK           = "192.168.50."
NETMASK           = "255.255.255.0"

# Default Virtualbox .box
# TODO: debian uyumlu diger sistemlerin denenmesi
BOX               = 'debian/jessie64'
BOX2               = 'debian/stretch64'

HOSTS = {
  "db" => [NETWORK+"11", RAM, GUI, BOX],
  "ldap" => [NETWORK+"12", RAM, GUI, BOX],
  "im" => [NETWORK+"13", RAM, GUI, BOX],
  "fileserver" => [NETWORK+"14", RAM, GUI, BOX],
  "lider" => [NETWORK+"10", RAM, GUI, BOX],
  "ahenk" => [NETWORK+"15", 2048, true, BOX2],
  "console" => [NETWORK+"16", 4096, true, BOX2],
}



Vagrant.configure("2") do |config|
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.manage_guest = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
#     config.disksize.size = '20GB'

    # Sanal makinalari olusturuyorum
    HOSTS.each do | (name, cfg) |
      ipaddr, ram, gui, box = cfg

      config.vm.define name do |machine|
        machine.vm.box   = box
        machine.vm.guest = :debian

        machine.vm.provider "virtualbox" do |vbox|
          vbox.gui    = gui
          vbox.memory = ram
          vbox.name = name
        end

        machine.vm.hostname = name + DOMAIN
        machine.vm.network 'private_network', ip: ipaddr, netmask: NETMASK
#         machine.vm.network "public_network", use_dhcp_assigned_default_route: true
        machine.hostmanager.aliases = [name ]
      end
    end # HOSTS-each


    # hostmanager provisioner
    config.vm.provision :hostmanager

   # provision the host with ansible
    config.vm.provision :ansible do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "ansible/inventory"

      ansible.become = true
#       ansible.compatibility_mode = "1.8"
    end

end
