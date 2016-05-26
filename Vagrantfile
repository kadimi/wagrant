# -*- mode: ruby -*-
# vi: set ft=ruby :


## SETUP
#
# 1. Run vagrant up
# 2. Choose Home or Work network location
# 3. Run in `cmd` with elevated privileges:
#      @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://git.io/vr64y'))"
# 4. ...
#
#
## RESOURCES
#
# http://stackoverflow.com/a/35721868
# http://support.auvik.com/hc/en-us/articles/204610500-How-to-enable-WMI-monitoring-on-a-single-Windows-device
# https://github.com/mitchellh/vagrant/issues/6430
# https://gist.github.com/andreptb/57e388df5e881937e62a
# https://gist.github.com/sneal/39d47401e9eaefcf8727
#
##


# box name into env var, same script can be used with different boxes. Defaults to win7-ie11.
box_name = box_name = ENV['box_name'] != nil ? ENV['box_name'].strip : 'win7-ie11'
# box repo into env var, so private repos/cache can be used. Defaults to http://aka.ms
box_repo = ENV['box_repo'] != nil ? ENV['box_repo'].strip : 'http://aka.ms'

Vagrant.configure("2") do |config|
  # If the box is win7-ie11, the convention for the box name is modern.ie/win7-ie11
  config.vm.box = "modern.ie/" + box_name
  # If the box is win7-ie11, the convention for the box url is http://aka.ms/vagrant-win7-ie11
  config.vm.box_url = box_repo + "/vagrant-" + box_name
  # big timeout since windows boot is slow and because we want enough time to enter commands on the first run
  config.vm.boot_timeout = 9999

  config.vm.guest = :windows

  config.vm.provision :shell, path: "./ps/Open-Ports.ps1"
  config.vm.provision :shell, path: "./ps/Install-Chocolatey.ps1"
  config.vm.provision :shell, path: "./ps/Install-Apps.ps1"

  # Hostname
  config.vm.hostname = 'wagarnt'

  # Port forwarding
  config.vm.network "forwarded_port", guest: 3389, host: 3389, id: "rdp", auto_correct: true
  config.vm.network :forwarded_port, guest: 5985, host: 5985, id: "winrm", auto_correct: true

  # Second network interface, it must be public in order to get a static IP
  # config.vm.network :public_network, ip: "192.168.1.88", :adapter => 2


  # winrm config, uses modern.ie default user/password. If other credentials are used must be changed here
  config.vm.communicator = "winrm"
  config.winrm.username = "IEUser"
  config.winrm.password = "Passw0rd!"
  # Fix HTTPClient::KeepAliveDisconnected
  config.winrm.retry_limit = 30
  config.winrm.retry_delay = 10

  config.vm.provider "virtualbox" do |vb|
    # first setup requires gui to be enabled so scripts can be executed in virtualbox guest screen
    vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "2024"]
    vb.customize ["modifyvm", :id, "--vram", "128"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # vb.customize ["modifyvm", :id, "--natnet1", "192.168.80.0/24"]
  end
end