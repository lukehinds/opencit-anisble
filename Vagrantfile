# Runs the role against CentOS 7
# for local testing purposes

Vagrant.configure("2") do |config|
  config.vm.define "centos7" do |centos7|
    centos7.vm.box = "centos/7"
    centos7.vm.hostname = "opencit"
    centos7.vm.provision "ansible_local" do |ansible|
      ansible.groups = {
        "opencit" => ["default"]
      }
      ansible.galaxy_role_file = "/vagrant/requirements.yml"
      ansible.playbook = "playbook.yml"
    end
  end
end
