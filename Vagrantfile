Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"

  config.vm.provider :virtualbox do |vb|
    vb.gui = true
    vb.cpus = 2
    vb.memory = 2048
  end

  config.vm.provision "shell" do |s|
    s.name = "Save some memory"
    s.inline = "systemctl stop unattended-upgrades && apt remove -y unattended-upgrades"
  end

  config.vm.provision "shell" do |s|
    s.name = "Fix to allow login from gui"
    s.inline = "echo 'vagrant:vagrant' | chpasswd"
  end

  config.vm.provision "shell" do |s|
    s.name = "Install everything"
    s.inline = "apt update && apt install -y openbox obconf tint2 xinit htop byobu firefox-esr xterm"
  end

  config.vm.provision "shell" do |s|
    s.name = "Allow x11 for vagrant"
    s.inline = "sed -i 's/allowed_users=.*/allowed_users=anybody/' /etc/X11/Xwrapper.config"
  end

  config.vm.provision "shell" do |s|
    s.name = "Copy .xinitrc to ~"
    s.privileged = false
    s.inline = "cp -avf /vagrant/.xinitrc /home/vagrant/.xinitrc"
  end

  config.vm.provision "shell" do |s|
    s.name = "Copy .Xdefaults to ~"
    s.privileged = false
    s.inline = "cp -avf /vagrant/.Xdefaults /home/vagrant/.Xdefaults"
  end
end
