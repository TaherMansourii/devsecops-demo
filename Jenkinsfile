# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base box
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "devops-pipeline"

  # Forward ports to host (only listen on localhost / 127.0.0.1)
  # Jenkins web UI
  config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1", auto_correct: true
  # Alternative host mapping (if you need to run another service on host:8080)
  config.vm.network "forwarded_port", guest: 8080, host: 8081, host_ip: "127.0.0.1", auto_correct: true
  # Jenkins agent (JNLP)
  config.vm.network "forwarded_port", guest: 50000, host: 50000, host_ip: "127.0.0.1", auto_correct: true
  # HTTP (if you host other web apps on port 80 inside guest)
  config.vm.network "forwarded_port", guest: 80, host: 8082, host_ip: "127.0.0.1", auto_correct: true
  # SSH (useful for direct ssh if needed; Vagrant defaults to its own mapping but explicit helps)
  config.vm.network "forwarded_port", guest: 22, host: 2222, host_ip: "127.0.0.1", id: "ssh", auto_correct: true

  # Private network (optional) — reachable from host at 192.168.56.10
  config.vm.network "private_network", ip: "192.168.56.10"

  # Shared folder: host project folder -> guest
  config.vm.synced_folder ".", "/home/vagrant/projects", type: "virtualbox"

  # Provider-specific settings (VirtualBox)
  config.vm.provider "virtualbox" do |vb|
    vb.name = "devops-pipeline-ubuntu"
    vb.memory = 4096
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    # vb.gui = true   # uncomment to see VM GUI
  end

  # Insert generated SSH key (prevents Vagrant from replacing the default insecure key)
  config.ssh.insert_key = true

  # Optional: Always run this small provisioning to ensure basic tooling (uncomment if you want automatic setup)
  # config.vm.provision "shell", privileged: true, inline: <<-SHELL
  #   export DEBIAN_FRONTEND=noninteractive
  #   apt-get update -y
  #   apt-get install -y curl wget git openjdk-17-jdk maven docker.io
  #   usermod -aG docker vagrant || true
  #   systemctl enable --now docker || true
  # SHELL
end
