# -*- mode: ruby -*-
# vi: set ft=ruby :

# Specify minimum Vagrant version and Vagrant API version
Vagrant.require_version '>= 1.9.5'
VAGRANT_API_VERSION = '2'

# Require 'yaml' module
require 'yaml'

# Read YAML file with VM details (box, CPU, RAM, IP addresses)
# Edit VagrantMachines.yml to change VM configuration details
machines = YAML.load_file(File.join(File.dirname(__FILE__), 'VagrantMachines.yml'))
debops_docker_hosts = machines.select {|m| m['debops_groups'].include? 'debops_docker_hosts' }

Vagrant.configure(VAGRANT_API_VERSION) do |config|

  # Use Vagrant's default insecure ssh key
  config.ssh.insert_key = false

  # Iterate through entries in YAML file to create VMs
  machines.each do |machine|
    config.vm.define machine['name'] do |srv|
      srv.vm.box = machine['box']
      srv.vm.hostname = machine['name']

      # Disable default synced folder
      srv.vm.synced_folder '.', '/vagrant', disabled: true

      # Configure the VM with RAM and CPUs per VagrantMachines.yml (VirtualBox)
      srv.vm.provider 'virtualbox' do |vb, override|
        vb.gui = false
        vb.memory = machine['ram']
        vb.cpus = machine['vcpu']
        vb.customize ["modifyvm", :id, "--groups", machine['vb_group']]
      end # srv.vm.provider virtualbox

      # Enable provisioning with a shell script. Additional provisioners such as
      # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
      # documentation for more information about their specific syntax and use.
      # srv.vm.provision "shell", inline: <<-SHELL
      #   apt-get update
      # SHELL

      # Dynamically create/update ansible inventory file
      srv.vm.provision "vai" do |ansible|
        ansible.inventory_dir = 'ansible/inventory'
        ansible.inventory_filename='hosts_vagrant'
        ansible.groups = {
          'debops_all_hosts' => machines.map {|m| m['name'] },
          'debops_docker_hosts' => debops_docker_hosts.map {|m| m['name'] }
        }
      end

      # srv.vm.post_up_message = '
      # '

    end # config.vm.define
  end # machines.each
end
