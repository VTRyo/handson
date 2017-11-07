# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos6-4"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.4.2/centos64-x86_64-20140116.box"

  config.vm.define :web_server do |web_server|
    web_server.vm.network :forwarded_port, id: "ssh", guest: 22, host: 2222
    web_server.vm.network :forwarded_port, id: "http", guest: 80, host: 8080
    web_server.vm.network :private_network, ip: "192.168.33.10"

    web_server.vm.synced_folder ".", "/vagrant"
      :owner => "vagrant", :group => "vagrant",
      :mount_options => ["dmode=777,fmode=777"]
      
    web_server.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "ansible/playbook.yml"
      ansible.extra_vars = {
      	"PHP_VERSION_EPEL"	=> "https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm",
      	"PHP_VERSION_REMI"	=> "http://rpms.famillecollet.com/enterprise/remi-release-6.rpm",
	"MYSQL_VERSION"		=> "http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm",
      	"h2o_conf_user"		=> "nobody"
      }
    end
  end
end
