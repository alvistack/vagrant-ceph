# Vagrant Box Packaging for Ceph

[![Travis](https://img.shields.io/travis/com/alvistack/vagrant-ceph.svg)](https://travis-ci.com/alvistack/vagrant-ceph)
[![GitHub release](https://img.shields.io/github/release/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/releases)
[![GitHub license](https://img.shields.io/github/license/alvistack/vagrant-ceph.svg)](https://github.com/alvistack/vagrant-ceph/blob/master/LICENSE)
[![Vagrant Box](https://img.shields.io/badge/vagrant-alvistack/ceph-blue.svg)](https://app.vagrantup.com/alvistack/boxes/ceph)

Ceph uniquely delivers object, block, and file storage in one unified system.

Learn more about Ceph: <https://ceph.io/>

## Supported Tags and Respective `Vagrantfile` Links

  - [`15.2`, `latest`](https://github.com/alvistack/vagrant-ceph/blob/master/molecule/15.2/Vagrantfile.j2)
  - [`14.2`](https://github.com/alvistack/vagrant-ceph/blob/master/molecule/14.2/Vagrantfile.j2)

## Overview

This Vagrant box makes it easy to get an instance of Ceph up and running.

Based on [Roboxes Vagrant Box](https://roboxes.org/) with:

  - Ubuntu 20.04 based
  - Base box running by [Vagrant Libvirt Provider](https://github.com/vagrant-libvirt/vagrant-libvirt)
  - Provision by [Ansible](https://www.ansible.com/) and [Molecule Vagrant Plugin](https://github.com/ansible-community/molecule-vagrant)

### Quick Start

### Bootstrap Vagrant and Libvirt

Start by cloning the repository, checkout the corresponding branch, then bootstrap Vagrant and Libvirt with provided helper script:

    # GIT clone the development branch
    git clone --branch develop https://github.com/alvistack/vagrant-ceph
    cd vagrant-ceph
    
    # Bootstrap Vagrant and Libvirt
    ./scripts/bootstrap-vagrant.sh

### Start Vagrant Box

How to use this box with Vagrant:

    # Initializes the current directory to be a Vagrant environment
    vagrant init alvistack/ceph
    
    # Creates and configures guest machines
    vagrant up

## Versioning

### `alvistack/ceph:<version>`

The version tags are rolling release rebuild by [Travis](https://travis-ci.com/alvistack/vagrant-ceph) in weekly basis. Thus using these tags will ensure you are running the latest packages provided by the base image project.

## License

  - Code released under [Apache License 2.0](LICENSE)
  - Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

## Author Information

  - Wong Hoi Sing Edison
      - <https://twitter.com/hswong3i>
      - <https://github.com/hswong3i>
