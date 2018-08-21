# Runs the role against RHEL 7.5

# subscription manager fix for rhel 7.5

module SubscriptionManagerMonkeyPatches
  def self.subscription_manager_registered?(machine)
    true if machine.communicate.sudo("/usr/sbin/subscription-manager list --consumed --pool-only | grep -E '^[a-f0-9]{32}$'")
  rescue
    false
  end
end

VagrantPlugins::Registration::Plugin.guest_capability 'redhat', 'subscription_manager_registered?' do
  SubscriptionManagerMonkeyPatches
end

Vagrant.configure("2") do |config|
  config.registration.username = 'lhinds@redhat.com'
  config.vm.synced_folder ".", "/vagrant", type: "nfs"
  config.vm.define "rhel7" do |rhel7|
    rhel7.vm.box = "generic/rhel7"
    rhel7.vm.hostname = "rhel7"
    rhel7.vm.provision "ansible_local" do |ansible|
      ansible.groups = {
        "rhel7" => ["default"]
      }
      ansible.galaxy_role_file = "requirements.yml"
      ansible.playbook = "playbook.yml"
    end
  end
end
