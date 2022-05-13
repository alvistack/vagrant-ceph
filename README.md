# Vagrant Box Packaging for Ceph

<img src="/alvistack.svg" width="75" alt="AlviStack">

[![Gitlab pipeline status](https://img.shields.io/gitlab/pipeline/alvistack/vagrant-ceph/master)](https://gitlab.com/alvistack/vagrant-ceph/-/pipelines)
[![GitHub tag](https://img.shields.io/github/tag/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/tags)
[![GitHub license](https://img.shields.io/github/license/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/blob/master/LICENSE) -[![Vagrant Box download](https://img.shields.io/badge/dynamic/json?label=alvistack%2Fceph-17.2&query=%24.boxes%5B%3A1%5D.downloads&url=https%3A%2F%2Fapp.vagrantup.com%2Fapi%2Fv1%2Fsearch%3Fq%3Dalvistack%2Fceph-17.2)](https://app.vagrantup.com/alvistack/boxes/ceph-17.2)

Ceph uniquely delivers object, block, and file storage in one unified system.

Learn more about Ceph: <https://ceph.io/>

## Supported Boxes and Respective Packer Template Links

  - [`alvistack/ceph-17.2`](https://app.vagrantup.com/alvistack/boxes/ceph-17.2)
      - [`libvirt`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/libvirt-17.2/packer.json)
      - [`virtualbox`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/virtualbox-17.2/packer.json)
  - [`alvistack/ceph-16.2`](https://app.vagrantup.com/alvistack/boxes/ceph-16.2)
      - [`libvirt`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/libvirt-16.2/packer.json)
      - [`virtualbox`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/virtualbox-16.2/packer.json)
  - [`alvistack/ceph-15.2`](https://app.vagrantup.com/alvistack/boxes/ceph-15.2)
      - [`libvirt`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/libvirt-15.2/packer.json)
      - [`virtualbox`](https://github.com/alvistack/vagrant-ceph/blob/master/packer/virtualbox-15.2/packer.json)

## Overview

  - Packaging with [Packer](https://www.packer.io/)
  - Support [Vagrant](https://www.vagrantup.com/) as default [Ceph custom executor](https://docs.gitlab.com/runner/executors/README.html)
  - Support [Libvirt](https://libvirt.org/) with [vagrant-libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt)
  - Support [VirtualBox](https://www.virtualbox.org/)
  - Support [Docker](https://www.docker.com/)

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

## Versioning

### `YYYYMMDD.Y.Z`

Release tags could be find from [GitHub Release](https://github.com/alvistack/vagrant-ceph/tags) of this repository. Thus using these tags will ensure you are running the most up to date stable version of this image.

### `YYYYMMDD.0.0`

Version tags ended with `.0.0` are rolling release rebuild by [GitLab pipeline](https://gitlab.com/alvistack/vagrant-ceph/-/pipelines) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

  - Code released under [Apache License 2.0](LICENSE)
  - Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

  - Wong Hoi Sing Edison
      - <https://twitter.com/hswong3i>
      - <https://github.com/hswong3i>
