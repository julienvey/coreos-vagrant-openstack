require 'vagrant-openstack-provider'
require 'Base64'

Vagrant.configure('2') do |config|

  config.vm.box       = 'dummy-openstack'
  config.vm.box_url   = 'https://github.com/ggiamarchi/vagrant-openstack/raw/master/source/dummy.box'

  config.ssh.username = ENV['OS_SSH_USERNAME']

  config.vm.provider :openstack do |os|
    os.username           = ENV['OS_USERNAME']
    os.password           = ENV['OS_PASSWORD']
    os.flavor             = ENV['OS_FLAVOR']
    os.image              = ENV['OS_IMAGE']
    os.openstack_auth_url = ENV['OS_AUTH_URL']
    os.tenant_name        = ENV['OS_TENANT_NAME']
    os.sync_method        = 'none'
  end

  (1..4).each do |i|
    config.vm.define "instance_#{i}" do |instance|
      instance.vm.provider :openstack do |os|
        os.server_name      = "coreos-#{i}"
        os.floating_ip_pool = ENV['OS_FLOATING_IP_POOL']
        os.user_data = Base64.encode64("manage-resolv-conf: true

resolv_conf:
  nameservers: ['8.8.4.4', '8.8.8.8']

coreos:
  etcd:
    discovery: https://discovery.etcd.io/#{ENV['ETCD_TOKEN']}
    # multi-region and multi-cloud deployments need to use $public_ipv4
    addr: $private_ipv4:4001
    peer-addr: $private_ipv4:7001
  units:
    - name: etcd.service
      command: start
    - name: fleet.service
      command: start")
      end
    end
  end
end
