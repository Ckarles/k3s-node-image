# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "arm64" do |alpine_aarch64|
    alpine_aarch64.vm.box = "../alpine-image/dist/alpine-image-vagrant_aarch64/alpine_aarch64.box"

    alpine_aarch64.vm.provider :libvirt do |libvirt|
      libvirt.loader = "/usr/share/edk2/aarch64/QEMU_CODE.fd"
      libvirt.nvram = "../alpine-image/dist/alpine-image-vagrant_aarch64/efivars.fd"
    end
  end

  config.vm.define "amd64" do |alpine_x86_64|
    alpine_x86_64.vm.box = "../alpine-image/dist/alpine-image-vagrant_x86_64/alpine_x86_64.box"

    alpine_x86_64.vm.provider :libvirt do |libvirt|
      libvirt.loader = "/usr/share/edk2/x64/OVMF_CODE.fd"
      libvirt.nvram = "../alpine-image/dist/alpine-image-vagrant_x86_64/efivars.fd"
    end
  end
  
  config.vm.provider :libvirt do |libvirt|
    libvirt.cpus = 2
    libvirt.memory = 2048
  end

  config.vm.network :private_network, :type => "dhcp", :libvirt__forward_mode => "none", auto_config: false

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible-playbook.yml"
  end
end
