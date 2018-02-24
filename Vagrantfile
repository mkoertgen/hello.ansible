# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.box = 'envimation/ubuntu-xenial'

  # just in case there is a HTTP_PROXY configured for the host
  # system, the virtual machine is going to use it
  if ENV.key? 'http_proxy'
    if Vagrant.has_plugin? 'vagrant-proxyconf'
      proxy = ENV['http_proxy']
      config.proxy.http = proxy
      config.proxy.https = ENV.fetch('https_proxy') { proxy }
      config.proxy.no_proxy = ENV.fetch('no_proxy') { 'localhost,127.0.0.1' }
    else
      print "  WARN: Missing plugin 'vagrant-proxyconf'.\n"
      print "  Use 'vagrant plugin install vagrant-proxyconf' to install.\n"
      print "  You might need to set http_proxy to do this, however.\n"
    end
  end

  if Vagrant.has_plugin? 'vagrant-cachier'
    # machine scope, cf.: http://fgrehm.viewdocs.io/vagrant-cachier/usage/
    config.cache.scope = :machine
  else
    print "  WARN: Missing plugin 'vagrant-cachier'.\n"
    print "  Use 'vagrant plugin install vagrant-cachier' to install.\n"
  end

  config.vbguest.auto_update = false if Vagrant.has_plugin? 'vagrant-vbguest'

  # config.vm.provider :virtualbox do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = '1024'
  # end
  #

  # cf.:
  # - https://www.vagrantup.com/docs/provisioning/ansible.html
  # - https://www.vagrantup.com/docs/provisioning/ansible_intro.html
  # - https://www.vagrantup.com/docs/provisioning/ansible_common.html
  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'ansible/site.yml'
    ansible.compatibility_mode = '2.0'
    ansible.version = '2.4.3.0'

    # install role dependencies from ansible galaxy
    ansible.galaxy_role_file = 'ansible/requirements.yml'
    ansible.galaxy_roles_path = 'ansible/roles'
    ansible.galaxy_command = 'ansible-galaxy install -r %<role_file>s -p %<roles_path>s'

    # ansible.host_key_checking = 'false'
    # ansible.verbose = 'v'
    # ansible.config_file = 'ansible/ansible.cfg'

    # Use a hand-crafted inventory
    # ansible.inventory_path = 'ansible/inventories/vagrant'

    # ansible.vault_password_file =
  end
end
