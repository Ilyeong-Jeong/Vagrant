# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

# Vagrant Version
Vagrant.configure(2) do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # Vagrant Cloud에서 이미지를 다운로드 및 실행
  config.vm.box = "ubuntu/xenial64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # Port Forwarding 웹 서버를 사용하기 위한 포트 설정
  config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 8989, host: 8989, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 6767, host: 6767, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 9000, host: 9000, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # 가상 머신의 IP를 아래 설정한 IP주소에 할당
  #config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  #config.vm.network "public_network", use_dhcp_assigned_default_route: true
 
  config.vm.network "public_network", :bridge => "eth0", auto_config: false
  
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
 
  # 공유 폴더 설정 - 본인 경로에 맞춰서 수정
  config.vm.synced_folder "/Users/user/Documents/repos", "/home/vagrant/dev/repos"
  
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  # 가상 머신 provider 지정 및 하드웨어 설정
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory    = "4096"
     vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  # View the documentation for the provider you are using for more
  # information on available options.
 
  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end
 
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # provision 설정
  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
     sudo apt-get install -y curl
     sudo curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
     sudo apt-get install -y nodejs
     sudo apt-get install -y git
     sudo apt-get install -y libssl-dev
     sudo curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
     sudo echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn
     sudo apt-get install -yq gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 \
      libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 \
      libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 \
      libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 \
      ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget
     sudo npm install webpack -g
     sudo npm install webpack-dev-server -g
     sudo npm install gulp -g
     sudo npm install lerna -g
  SHELL
end