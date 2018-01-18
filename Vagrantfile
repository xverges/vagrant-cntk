# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "forwarded_port", guest: 8888, host: 8888, auto_correct: true
  
  config.vm.provider "virtualbox" do |vb|

    #From https://stefanwrobel.com/how-to-make-vagrant-performance-not-suck#use-1-4-system-memory

    host = RbConfig::CONFIG['host_os']

    # Give VM 1/4 system memory
    if host =~ /darwin/
        # sysctl returns Bytes and we need to convert to MB
        mem = `sysctl -n hw.memsize`.to_i / 1024
    elsif host =~ /linux/
        # meminfo shows KB and we need to convert to MB
        mem = `grep 'MemTotal' /proc/meminfo | sed -e 's/MemTotal://' -e 's/ kB//'`.to_i
    elsif host =~ /mswin|mingw|cygwin/
        # Windows code via https://github.com/rdsubhas/vagrant-faster
        mem = `wmic computersystem Get TotalPhysicalMemory`.split[1].to_i / 1024
    end

    mem = mem / 1024 / 4
    vb.customize ["modifyvm", :id, "--memory", mem]
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    cd /vagrant
    sudo apt-get update
    sudo apt-get --assume-yes install \
        curl \
        openmpi-bin

    if [[ ! -f $miniconda.sh ]]; then
        wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.3.31-Linux-x86_64.sh -O miniconda.sh
    fi
    chmod +x miniconda.sh
    ./miniconda.sh -b -p /home/vagrant/anaconda

    echo 'PATH=/home/vagrant/anaconda/bin:\$PATH' >> /home/vagrant/.bashrc
    PATH=/home/vagrant/anaconda/bin:$PATH

    # Python 3.6.2 breaks dynamic linkking https://github.com/ContinuumIO/anaconda-issues/issues/6401
    conda install --yes python=3.6.1 jupyter=1.0.0
    pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.3.1-cp36-cp36m-linux_x86_64.whl
    pip install pytest
    python -c "import cntk; print(cntk.__version__)"
  SHELL



end
