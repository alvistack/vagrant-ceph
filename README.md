# Vagrant Box Packaging for Ceph

[![Gitlab pipeline status](https://img.shields.io/gitlab/pipeline/alvistack/vagrant-ceph/master)](https://gitlab.com/alvistack/vagrant-ceph/-/pipelines)
[![GitHub release](https://img.shields.io/github/release/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/releases)
[![GitHub license](https://img.shields.io/github/license/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/blob/master/LICENSE)
\-[![Vagrant Box download](https://img.shields.io/badge/dynamic/json?label=alvistack%2Fceph-16.2&query=%24.boxes%5B%3A1%5D.downloads&url=https%3A%2F%2Fapp.vagrantup.com%2Fapi%2Fv1%2Fsearch%3Fq%3Dalvistack%2Fceph-16.2)](https://app.vagrantup.com/alvistack/boxes/ceph-16.2)

Ceph uniquely delivers object, block, and file storage in one unified system.

Learn more about Ceph: <https://ceph.io/>

## Supported Boxes and Respective Packer Template Links

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
    vagrant init alvistack/ceph-16.2
    
    # Start the virtual machine
    vagrant up
    
    # SSH into this machine
    vagrant ssh
    
    # Terminate the virtual machine
    vagrant destroy --force

## Versioning

### `YYYYMMDD.Y.Z`

Release tags could be find from [GitHub Release](https://github.com/alvistack/vagrant-ceph/releases) of this repository. Thus using these tags will ensure you are running the most up to date stable version of this image.

### `YYYYMMDD.0.0`

Version tags ended with `.0.0` are rolling release rebuild by [GitLab pipeline](https://gitlab.com/alvistack/vagrant-ceph/-/pipelines) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

  - Code released under [Apache License 2.0](LICENSE)
  - Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

  - Wong Hoi Sing Edison
      - <https://twitter.com/hswong3i>
      - <https://github.com/hswong3i>
