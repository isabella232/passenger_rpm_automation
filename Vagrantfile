# -*- mode: ruby -*-
# vi: set ft=ruby :
ROOT = File.dirname(File.expand_path(__FILE__))

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "phusion-open-ubuntu-12.04-amd64"
  config.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/ubuntu-12.04.3-amd64-vbox.box"
  config.ssh.forward_agent = true

  config.vm.provider :vmware_fusion do |f, override|
    override.vm.box_url = "https://oss-binaries.phusionpassenger.com/vagrant/boxes/ubuntu-12.04.3-amd64-vmwarefusion.box"
    f.vmx["displayName"] = "baseimage-docker"
  end

  # Add lxc-docker package
  pkg_cmd = "if [[ -e /usr/bin/docker ]]; then exit; fi; " \
    "wget -q -O - https://get.docker.io/gpg | apt-key add -;" \
    "echo deb http://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list;" \
    "apt-get update -qq; apt-get install -q -y --force-yes lxc-docker; "
  # Add vagrant user to the docker group
  pkg_cmd << "usermod -a -G docker vagrant; "
  config.vm.provision :shell, :inline => pkg_cmd
end