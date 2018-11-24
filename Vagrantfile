# -*- mode: ruby -*-
# vi: set ft=ruby :

MINUTE = 60

# box name into env var, same script can be used with different boxes. Defaults to win7-ie11.
box_name = box_name = ENV['box_name'] != nil ? ENV['box_name'].strip : 'ie11.win7.vagrant'
# box repo into env var, so private repos/cache can be used. Defaults to http://aka.ms
box_repo = ENV['box_repo'] != nil ? ENV['box_repo'].strip : 'http://aka.ms'

Vagrant.configure("2") do |config|

  ## Box
  config.vm.box = "modern.ie/" + box_name
  config.vm.box_url = box_repo + "/" + box_name


  ## System
  config.vm.guest = :windows
  config.vm.boot_timeout = 30 * MINUTE


  ## Provisioning
  config.vm.provision :shell, path: "./ps/Open-Ports.ps1"
  config.vm.provision :shell, path: "./ps/Install-Chocolatey.ps1"
  config.vm.provision :shell, path: "./ps/Install-Apps.ps1"


  ## Network
  config.vm.hostname = 'wagrant'
  config.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
  config.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true
  config.vm.network :private_network, ip: "192.168.50.88", :adapter => 2
  # config.vm.network :public_network, ip: "192.168.1.88", :adapter => 3


  ## Remote Access (WinRM)
  # winrm config, uses modern.ie default username and password.
  config.vm.communicator = "winrm"
  config.winrm.username = "IEUser"
  config.winrm.password = "Passw0rd!"
  # Fix HTTPClient::KeepAliveDisconnected
  config.winrm.retry_limit = 30
  config.winrm.retry_delay = 10

  ## Other
  config.vm.provider "virtualbox" do |vb|
    # first setup requires gui to be enabled so scripts can be executed in virtualbox guest screen
    vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--vram", "256"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']
  end
end
