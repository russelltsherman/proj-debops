# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'rbconfig'
require 'yaml'

# Specify minimum Vagrant version and Vagrant API version
VAGRANT_MIN_VERSION = '>= 1.9.5'
VAGRANTFILE_API_VERSION = '2'
# Set your default base box here
DEFAULT_BASE_BOX = 'ubuntu/xenial64'
# Set Project name
PROJECT_NAME = '/' + File.basename(Dir.getwd)

NET_INT = 'enp0s3'

# Read YAML file with VM details (box, CPU, RAM, IP addresses)
# Edit VagrantMachines.yml to change VM configuration details
machines = YAML.load_file(File.join(File.dirname(__FILE__), 'VagrantMachines.yml'))

# Set options for the network interface configuration. All values are
# optional, and can include:
# - ip (default = DHCP)
# - netmask (default value = 255.255.255.0
# - mac
# - auto_config (if false, Vagrant will not configure this network interface
# - intnet (if true, an internal network adapter will be created instead of a
#   host-only adapter)
def network_options(nw)
  options = {}

  if nw.key?('ip')
    options[:ip] = nw['ip']
    options[:netmask] = nw['netmask'] ||= '255.255.255.0'
  else
    options[:type] = 'dhcp'
  end

  options[:mac] = nw['mac'].gsub(/[-:]/, '') if nw.key?('mac')
  options[:auto_config] = nw['auto_config'] if nw.key?('auto_config')
  options[:virtualbox__intnet] = true if nw.key?('intnet')
  options
end

Vagrant.require_version VAGRANT_MIN_VERSION
Vagrant.configure(VAGRANT_API_VERSION) do |config|

  # Use Vagrant's default insecure ssh key
  config.ssh.insert_key = false

  # Iterate through entries in YAML file to create VMs
  machines.each do |host|
    config.vm.define host['hostname'] do |node|
      node.vm.box = (host['box'] ||= DEFAULT_BASE_BOX)
      node.vm.box_url = host['box_url'] if host.key? 'box_url'

      node.vm.hostname = host['hostname'] if host.key? 'hostname'
      node.vm.network 'public_network', network_options(host['network']['public'])
      node.vm.network 'private_network', network_options(host['network']['private'])

      # Disable default synced folder
      node.vm.synced_folder '.', '/vagrant', disabled: true

      if host.has_key?('synced_folders')
        host['synced_folders'].each do |folder|
          vm.synced_folder folder['src'], folder['dest'], folder['options']
        end
      end

      if host.has_key?('shell_always')
        host['shell_always'].each do |script|
          vm.provision "shell", inline: script['cmd'], run: "always"
        end
      end

      if host.has_key?('forwarded_ports')
        host['forwarded_ports'].each do |port|
          vm.network "forwarded_port", guest: port['guest'], host: port['host']
        end
      end

      # Configure the VM with RAM and CPUs per VagrantMachines.yml (VirtualBox)
      node.vm.provider 'virtualbox' do |vb, override|
        vb.gui = false
        vb.cpus = (host['cpus'] || '1')
        vb.memory = (host['memory'] || '512')
        vb.customize ["modifyvm", :id, "--groups", host['vb_group']]
      end # node.vm.provider virtualbox

      # default router
      node.vm.provision "shell", inline: <<-SHELL
        sudo route add default gw #{host['network']['public']['gateway']}
      SHELL

      # delete default gw on #{NET_INT}
      node.vm.provision "shell", inline: <<-SHELL
        eval `route -n | awk '{ if ($8 =="#{NET_INT}" && $2 != "0.0.0.0") print "sudo route del default gw " $2; }'`
      SHELL

      # Enable provisioning with a shell script. Additional provisioners such as
      # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
      # documentation for more information about their specific syntax and use.
      node.vm.provision "shell", inline: <<-SHELL
        ifconfig
        route
      SHELL

      # Dynamically create/update ansible inventory file
      node.vm.provision "vai" do |ansible|
        ansible.inventory_dir = 'ansible/inventory'
        ansible.inventory_filename='hosts_vagrant'
        ansible.groups = {
					'debops_all_hosts' => machines.map {|m| m['name'] },
        }
      end

      # node.vm.post_up_message = '
      # '

    end # config.vm.define
  end # machines.each
end
