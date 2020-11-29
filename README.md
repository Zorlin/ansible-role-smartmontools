Ansible Role: Smartmontools
=========

![CI](https://github.com/Zorlin/ansible-role-smartmontools/workflows/CI/badge.svg)

This role automatically configures and installs a relatively recent (at least v7) version of smartmontools.

While this software is available in most repositories, it's often outdated. Software such as [Scrutiny](https://github.com/AnalogJ/scrutiny) relies on having at least smartmontools v7 installed. This role aims to achieve that while being available for all platforms someone could reasonably want to run on.

Currently this includes:

* CentOS 6, CentOS 7, CentOS 8 (should also work with RHEL)
* Debian 9 and Debian 10
* Ubuntu 16.04, Ubuntu 18.04, Ubuntu 20.04

Requirements
------------

Before this role runs, you need to make sure the following dependencies are installed:

| Dependency                    | Suggested Role           |
| ----------------------------- | ------------------------ |
| EPEL repo (RedHat OSes only)  | `geerlingguy.repo-epel`  |
| Git                           | `geerlingguy.git`        |

See this role's [`molecule/default/converge.yml`](molecule/default/converge.yml) playbook for an example that works across many different OSes.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    smartmontools_install_from_backports: false
    smartmontools_install_systemd_stuff: true
    smartmontools_install_selinux_stuff: true
    smartmontools_src_location: "/usr/local/src/smartmontools"

By default, this role will opt to build from source instead of installing from backports if a recent smartmontools is only available from backports. You can tell the role to install from backports when available by changing setting `smartmontools_install_from_backports` to `true`. **NOTE:** This role may default to installing from backports in the future.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- name: Install smartmontools
  hosts: all
  become: true

  roles:
    - role: geerlingguy.repo-epel
      when: ansible_os_family == 'RedHat'
    - geerlingguy.git
    - zorlin.smartmontools
```

License
-------

MIT

Author Information
------------------

This role was created in 2020 by Benjamin Arntzen.

This role uses examples and code from [geerlingguy.awx](https://github.com/geerlingguy/ansible-role-awx) which was written by Jeff Geerling.

TODOs
-----

* Add a flag to always build from source
* Investigate co-existing with smartmontools < 7
