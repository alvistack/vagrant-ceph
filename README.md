# Vagrant Box Packaging for Ceph

<a href="https://alvistack.com" title="AlviStack" target="_blank"><img src="/alvistack.svg" height="75" alt="AlviStack"></a>

[![Gitlab pipeline status](https://img.shields.io/gitlab/pipeline/alvistack/vagrant-ceph/master)](https://gitlab.com/alvistack/vagrant-ceph/-/pipelines)
[![GitHub tag](https://img.shields.io/github/tag/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/tags)
[![GitHub license](https://img.shields.io/github/license/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/blob/master/LICENSE) -[![Vagrant Box download](https://img.shields.io/badge/dynamic/json?label=alvistack%2Fceph-17.2&query=%24.boxes%5B%3A1%5D.downloads&url=https%3A%2F%2Fapp.vagrantup.com%2Fapi%2Fv1%2Fsearch%3Fq%3Dalvistack%2Fceph-17.2)](https://app.vagrantup.com/alvistack/boxes/ceph-17.2)

Ceph uniquely delivers object, block, and file storage in one unified system.

Learn more about Ceph: <https://ceph.io/>

## Supported Boxes and Respective Packer Template Links

-   [`alvistack/ceph-17.2`](https://app.vagrantup.com/alvistack/boxes/ceph-17.2)
    -   [`packer/ceph-17.2-libvirt/packer.json`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/ceph-17.2-libvirt/packer.json)
    -   [`ceph-17.2-virtualbox/packer.json`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/ceph-17.2-virtualbox/packer.json)
-   [`alvistack/ceph-16.2`](https://app.vagrantup.com/alvistack/boxes/ceph-16.2)
    -   [`packer/ceph-16.2-libvirt/packer.json`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/ceph-16.2-libvirt/packer.json)
    -   [`packer/ceph-16.2-virtualbox/packer.json`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/ceph-16.2-virtualbox/packer.json)
-   [`alvistack/ceph-15.2`](https://app.vagrantup.com/alvistack/boxes/ceph-15.2)
    -   [`packer/ceph-15.2-libvirt/packer.json`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/ceph-15.2-libvirt/packer.json)
    -   [`packer/ceph-15.2-virtualbox/packer.json`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/ceph-15.2-virtualbox/packer.json)

## Overview

-   Packaging with [Packer](https://www.packer.io/)
-   Minimal [Vagrant base box implementation](https://www.vagrantup.com/docs/boxes/base)
-   Support [QEMU Guest Agent](https://wiki.qemu.org/Features/GuestAgent)
-   Support [VirtualBox Guest Additions](https://www.virtualbox.org/manual/ch04.html)
-   Support [Vagrant synced folder with rsync](https://www.vagrantup.com/docs/synced-folders/rsync)
-   Support [Vagrant provisioner with Ansible](https://www.vagrantup.com/docs/provisioning/ansible)
-   Standardize disk partition with GPT
-   Standardize file system mount with UUID
-   Standardize network interface with `eth0`

### Quick Start

Once you have [Vagrant](https://www.vagrantup.com/docs/installation) and [VirtaulBox](https://www.virtualbox.org/) installed, run the following commands under your [project directory](https://learn.hashicorp.com/tutorials/vagrant/getting-started-project-setup?in=vagrant/getting-started):

    # Initialize Vagrant
    cat > Vagrantfile <<-EOF
    Vagrant.configure('2') do |config|
      config.vm.hostname = 'ceph-17.2'
      config.vm.box = 'alvistack/ceph-17.2'

      config.vm.provider :libvirt do |libvirt|
        libvirt.cpu_mode = 'host-passthrough'
        libvirt.cpus = 2
        libvirt.disk_bus = 'virtio'
        libvirt.disk_driver :cache => 'writeback'
        libvirt.driver = 'kvm'
        libvirt.memory = 8192
        libvirt.memorybacking :access, :mode => 'shared'
        libvirt.nested = true
        libvirt.nic_model_type = 'virtio'
        libvirt.storage :file, bus: 'virtio', cache: 'writeback'
        libvirt.video_type = 'virtio'
      end

      config.vm.provider :virtualbox do |virtualbox|
        config.vm.disk :disk, name: 'sdb', size: '10GB'
        virtualbox.cpus = 2
        virtualbox.customize ['modifyvm', :id, '--cpu-profile', 'host']
        virtualbox.customize ['modifyvm', :id, '--nested-hw-virt', 'on']
        virtualbox.memory = 8192
      end
    end
    EOF

    # Start the virtual machine
    export VAGRANT_EXPERIMENTAL='1'
    vagrant up

    # SSH into this machine
    vagrant ssh

    # Terminate the virtual machine
    vagrant destroy --force

### Molecule

You could also run our [Molecule](https://molecule.readthedocs.io/en/stable/) test cases if you have [Vagrant](https://www.vagrantup.com/) and [Libvirt](https://libvirt.org/) installed, e.g.

    # Run Molecule on Ceph 17.2
    molecule converge -s ceph-17.2-libvirt

Please refer to [.gitlab-ci.yml](.gitlab-ci.yml) for more information on running Molecule.

## Versioning

### `YYYYMMDD.Y.Z`

Release tags could be find from [GitHub Release](https://github.com/alvistack/vagrant-ceph/tags) of this repository. Thus using these tags will ensure you are running the most up to date stable version of this image.

### `YYYYMMDD.0.0`

Version tags ended with `.0.0` are rolling release rebuild by [GitLab pipeline](https://gitlab.com/alvistack/vagrant-ceph/-/pipelines) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

-   Code released under [Apache License 2.0](LICENSE)
-   Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

-   Wong Hoi Sing Edison
    -   <https://twitter.com/hswong3i>
    -   <https://github.com/hswong3i>
