# -*- mode: ruby -*-
# vi: set ft=ruby :

SPLUNK_HOME="/opt/splunk"
SPLUNK_SERVICE="/opt/splunk/bin/splunk"
FWDR_HOME="/opt/splunkforwarder"
FWDR_SERVICE="/opt/splunkforwarder/bin/splunk"

Vagrant.configure("2") do |config|
   config.vm.box = "centos/7"
   config.hostmanager.enable = false

   # Config definition for Splunk master.
   config.vm.define "splunk" do |splunk|
      splunk.vm.network "private_network", ip: "192.168.100.11"
      splunk.vm.hostname = "splunk.opswerks"
      splunk.vm.provision "shell", path: "scripts.d/centos"
      splunk.vm.provision "shell" do |s|
         s.path = "scripts.d/splunk"
         s.args = "admin"
         s.env = {
            :SPLUNK_HOME  => "#{SPLUNK_HOME}",
            :SPLUNK_SERVICE => "#{SPLUNK_SERVICE}"
         }
      end
      splunk.vm.provider :virtualbox do |vb| 
         vb.name = "splunk.opswerks"
      end
   end

   # Config definition for Splunk forwarder.
   config.vm.define "forwarder" do |forwarder|
      forwarder.vm.network "private_network", ip: "192.168.100.21"
      forwarder.vm.hostname = "splunkforwarder.opswerks"
      forwarder.vm.provision "shell", path: "scripts.d/centos"
      forwarder.vm.provision "shell" do |f|
         f.path = "scripts.d/splunkforwarder"
         f.args = "admin"
         f.env = {
            :FWDR_HOME  => "#{FWDR_HOME}",
            :FWDR_SERVICE => "#{FWDR_SERVICE}"
         }
      end
      forwarder.vm.provider :virtualbox do |vb|
         vb.name = "splunkforwarder.opswerks"
      end
   end

end
