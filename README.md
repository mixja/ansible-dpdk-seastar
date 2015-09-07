# Ansible Playbook to Build DPDK and Seastar on an Intel NUC

This playbook installs DPDK and Seastar on an Intel NUC.

See my blog post on [DPDK on an Intel NUC](http://pseudo.co.de/dpdk-on-an-intel-nuc/) for step-by-step instructions of the various tasks defined in this playbook.

## Quick Start
Ensure that you have [installed Ansible](http://docs.ansible.com/ansible/intro_installation.html) on the host where you want to run the playbook from.

To run the playbook against a host 192.168.1.100 (note the comma following the host name/IP address must be included):

```bash 
$ git clone https://github.com/mixja/ansible-dpdk-seastar.git 
...
...
$ cd ansible-dpdk-seastar
ansible-dpdk-seastar$ ansible-playbook -i "192.168.1.100," site.yml
SSH password: *******

PLAY [Provision Custom Facts] *************************************************
...
...
```

## Changing Folder and Repo Settings

The `group_vars/all` file contains the following variables:

- `dpdk_dir` - root folder of the DPDK source
- `dpdk_build` - build folder for the DPDK source
- `dpdk_repo` - Git repo of the DPDK source
- `seastar_dir` - root folder of the Seastar source
- `seastar_repo` - Git repo of the Seastar source

## Changing Build Settings

The following variables can be used to force a rebuild or build a different version:

- `seastar_rebuild` - if set to any value, forces Seastar to be built.
- `seastar_version` - specifies the branch, tag or commit hash to build.  If a change is detected from the current repo, Seastar will be rebuilt.
- `dpdk_rebuild` - if set to any value, forces DPDK to be built/

The following example forces DPDK to be built:

```bash
$ ansible-playbook -i "192.168.1.100," site.yml --extra-vars "dpdk_rebuild=true"
```

The following example checks out Seastar commit 696ab29 to be checked out and forces a build of Seastar:

```bash
$ ansible-playbook -i "192.168.1.100," site.yml --extra-vars "seastar_rebuild=true seastar_version=696ab29"
``` 

## Testing DPDK and Seastar

After DPDK and Seastar are built you need to:

- [Bind your NUC network interface to DPDK](http://pseudo.co.de/dpdk-on-an-intel-nuc/#binding-dpdk)
- [Run Seastar](http://pseudo.co.de/dpdk-on-an-intel-nuc/#running-seastar)
- [Test Seastar](http://pseudo.co.de/dpdk-on-an-intel-nuc/#testing-seastar)
