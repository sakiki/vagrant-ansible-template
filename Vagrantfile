# -*- mode: ruby -*-
# vi: set ft=ruby :

# Ensure yaml module is loaded
require 'yaml'

listedNodes = YAML.load_file('config.yml')

Vagrant.configure(2) do |config|
    listedNodes.each do |currentNode|

        config.vm.define currentNode["name"] do |nodeInstance|
            nodeInstance.vm.box = currentNode["imageName"]
            nodeInstance.vm.hostname = currentNode["name"]

            if currentNode["vagrantIp"] != nil
                nodeInstance.vm.network "private_network", ip: currentNode["vagrantIp"]
            end

            ansibleVars = currentNode["ansible"]

	    if ansibleVars != nil 

		nodeInstance.vm.provision "ansible" do |ansible|
		    if ansibleVars["playbook"] != nil
			ansible.playbook = ansibleVars["playbook"]
		    end
		    if ansibleVars["groups"] != nil
			ansible.groups = ansibleVars["groups"]
		    end
		    if ansibleVars["extraVars"] != nil
			ansible.extra_vars = ansibleVars["extraVars"]
		    end
		end

	    end

            nodeInstance.vm.provider "virtualbox" do |v|
                v.memory = currentNode["mem"]
                v.cpus = currentNode["cpu"]
            end

        end

    end
end
