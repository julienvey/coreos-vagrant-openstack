#Requirements

You need to upload a CoreOS image to your OpenStack cloud, see the [documentation](https://coreos.com/docs/running-coreos/platforms/openstack/#import-the-image)

#Usage

You will need the following environment variables to run you cluster

```bash
export OS_PASSWORD=password
export OS_AUTH_URL=http://mon.cloud.openstack/identity/v2.0/tokens
export OS_USERNAME=username
export OS_TENANT_NAME=tenant_name
export OS_FLOATING_IP_POOL=PublicNetwork
export OS_FLAVOR=m1.small
export OS_IMAGE=coreos
export OS_SSH_USERNAME=core
export ETCD_TOKEN=<token generated at https://discovery.etcd.io/new>
```

and then just run vagrant with the [vagrant-openstack-provider](https://github.com/ggiamarchi/vagrant-openstack-provider)

```bash
vagrant up --provider=openstack
```
