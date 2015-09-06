# Ansible Playbook to Build DPDK and Seastar on an Intel NUC

To run the playbook against a host 192.168.1.100 (note the comma following the host name/IP address must be included):

```console 
$ ansible-playbook -i "192.168.1.100," site.yml
```

The `group_vars/all` file contains the following variables:

- `dpdk_dir` - root folder of the DPDK source
- `dpdk_build` - build folder for the DPDK source
- `dpdk_repo` - Git repo of the DPDK source
- `seastar_dir` - root folder of the Seastar source
- `seastar_repo` - Git repo of the Seastar source
