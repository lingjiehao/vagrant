# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disabled: "true"
  # config.vm.network "forwarded_port", guest: 22, host: 22222

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "private_network", type: "dhcp"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Install vagrant-disksize to allow resizing the vagrant box disk.
  unless Vagrant.has_plugin?("vagrant-disksize")
    raise  Vagrant::Errors::VagrantError.new, "vagrant-disksize plugin is missing. Please install it using 'vagrant plugin install vagrant-disksize' and rerun 'vagrant up'"
  end

  config.disksize.size = '200GB'

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # vb.name = "my_vm"
    vb.memory = "4096"
    vb.cpus = 4
    vb.default_nic_type = "virtio"
    vb.check_guest_additions = false
  end

  # 替换sources.list
  config.vm.provision "shell", inline: <<-SHELL
    OS_VER=bionic
    MIRROR_URL=mirror.sjtu.edu.cn
    HTTP_OR_HTTPS=https
    cat <<EOF | tee /etc/apt/sources.list
deb ${HTTP_OR_HTTPS}://${MIRROR_URL}/ubuntu/ ${OS_VER} main restricted universe multiverse
deb ${HTTP_OR_HTTPS}://${MIRROR_URL}/ubuntu/ ${OS_VER}-updates main restricted universe multiverse
deb ${HTTP_OR_HTTPS}://${MIRROR_URL}/ubuntu/ ${OS_VER}-backports main restricted universe multiverse
deb ${HTTP_OR_HTTPS}://${MIRROR_URL}/ubuntu/ ${OS_VER}-security main restricted universe multiverse
# deb ${HTTP_OR_HTTPS}://${MIRROR_URL}/ubuntu/ ${OS_VER}-proposed main restricted universe multiverse
EOF
  SHELL

  # 安装Docker
  config.vm.provision "shell", path: "https://get.docker.com", args: "--mirror Aliyun"
  # config.vm.provision: docker

  # 配置虚拟机内代理
  # if Vagrant.has_plugin?("vagrant-proxyconf")
  #   config.proxy.http     = "http://192.168.90.103:10809"
  #   config.proxy.https    = "http://192.168.90.103:10809"
  #   config.proxy.no_proxy = "localhost,127.0.0.1"
  # end

end
