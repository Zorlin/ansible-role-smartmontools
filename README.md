Ansible Role: Smartmontools
=========

![CI](https://github.com/Zorlin/ansible-role-smartmontools/workflows/CI/badge.svg)

This role automatically configures and installs a relatively recent (at least v7) version of smartmontools.

While smartmontools packages are available in most repositories, they're often outdated. Software such as [Scrutiny](https://github.com/AnalogJ/scrutiny) relies on having at least smartmontools v7 installed. This role aims to achieve that while being available for all platforms someone could reasonably want to run on.

Currently this includes:

* CentOS 7 (should also work with RHEL)
* Debian 10, Debian 11
* Ubuntu 18.04, Ubuntu 20.04, Ubuntu 22.04

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

    smartmontools_install_from_source: true
    smartmontools_src_location: "/usr/local/src/smartmontools"

By default, this role will opt to install from backports rather than building from source if a recent smartmontools is available from backports. You can change this behaviour by changing setting `smartmontools_install_from_backports` to `false`. **NOTE:** This default may change in the future.

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