# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

  config.vm.provider "docker" do |d|

    d.build_dir	= "Docker"
    #d.cmd = ["/usr/sbin/cassandra" , "-f"]
    #usr/sbin/cassandra -- host {localhost} --port {9160}

    config.vm.network :forwarded_port, host: 9042, guest: 9042
    config.vm.network :forwarded_port, host: 9160, guest: 9160
  end

end
