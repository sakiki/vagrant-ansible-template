# -*- mode: ruby -*-
# vi: set ft=ruby :

# Ensure yaml module is loaded
require 'yaml'

listedNodes = YAML.load_file('vagrant-config.yml')

Vagrant.configure(2) do |config|
    listedNodes.each do |currentNode|

        config.vm.define currentNode["name"] do |nodeInstance|
            nodeInstance.vm.box = currentNode["imageName"]
            nodeInstance.vm.hostname = currentNode["name"]

            if currentNode["vagrantIp"] != "None"
                nodeInstance.vm.network "private_network", ip: currentNode["vagrantIp"]
            end

            nodeInstance.vm.provider "virtualbox" do |v|
                v.memory = currentNode["mem"]
                v.cpus = currentNode["cpu"]
            end

        end

    end
end