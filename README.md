[![Build Status](https://travis-ci.org/oasis-roles/rhv_answerfile_engine_setup.svg?branch=master)](https://travis-ci.org/oasis-roles/rhv_answerfile_engine_setup)

RHV ANSWERFILE ENGINE SETUP
===========

Install Red Hat Virtualization engine and configure it using an answerfile

Requirements
------------

Ansible 2.5 or higher

Red Hat Enterprise Linux 7 or equivalent

Valid Red Hat Subscriptions

Role Variables
--------------

Currently the following variables are supported:

### General

* `rhv_answerfile_engine_setup_package` - The package name to install on the remote hosts (set to `rhevm` by default)
* `rhv_answerfile_engine_setup_become_user` - The user to sign in as on the remote hosts (set to `root` by default)
* `rhv_answerfile_engine_setup_use_defaults` - Whether or not to accept the default answers to the engine-setup prompts (set to `true` by default)
* `rhv_answerfile_engine_setup_template_path` - The absolute or relative path to a file to use as a jinja2 template for generating an answerfile (not configured by default)
* `rhv_answerfile_engine_setup_host_hostname` - The hostname of the remote host. This gets used in rendering templates for an answerfile with engine-setup (not configured by default)
* `rhv_answerfile_engine_setup_host_domain` - The domain of the remote host. This gets used in rendering templates for an answerfile with engine-setup (not configured by default)
* `rhv_answerfile_engine_setup_engine_password` - The password to set for the engine (set to `d1r2o3w4s5s6a7p8` by default) **Note: The role may fail if the provided password does not meet the criteria of engine-setup**

<aside class="warning">
WARNING: AVOID USING THE DEFAULT ENGINE PASSWORD PROVIDED AS IT IS NOT SECURE AND EXISTS ONLY FOR DEMONSTRATION PURPOSES
</aside>

Dependencies
------------

This role requires that certain repositories be enabled to be able to install RHEVM and its dependencies. You may either use the [rhsm](https://galaxy.ansible.com/oasis-roles/rhsm) role from Ansible Galaxy or your own method of enabling the appropriate repos.

Example Playbook
----------------

Standalone
```yaml
- hosts: rhv_answerfile_engine_setup-servers
  roles:
    - role: oasis-roles.rhv_answerfile_engine_setup
      rhv_answerfile_engine_setup_use_defaults: true
      rhv_answerfile_engine_setup_engine_password: 123secure_password456
```

With an answerfile jinja2 template
```yaml
- hosts: rhv_answerfile_engine_setup-servers
  roles:
    - role: oasis-roles.rhv_answerfile_engine_setup
      rhv_answerfile_engine_setup_use_defaults: false
      rhv_answerfile_engine_setup_template_path: engine-setup-template  # This is a default template provided with the role. You may also specify a path to your own custom template
      rhv_answerfile_engine_setup_host_domain: host.domain.com
      rhv_answerfile_engine_setup_host_hostname: host.hostname.com
      rhv_answerfile_engine_setup_engine_password: 123secure_password456
```

With [rhsm](https://galaxy.ansible.com/oasis-roles/rhsm) from Ansible Galaxy
```yaml
- hosts: rhv_answerfile_engine_setup-servers
  roles:
    - role: oasis-roles.rhv_answerfile_engine_setup
      rhv_answerfile_engine_setup_use_defaults: true
      rhv_answerfile_engine_setup_engine_password: 123secure_password456
    - role: oasis-roles.rhsm
      rhsm_username: user@company.com
      rhsm_password: password
      rhsm_pool_ids:
        - abcdefghijklmnopqrstuvwxyz1234567890
      rhsm_repositories:
        only:
          - rhel-7-server-rpms
          - rhel-7-server-supplementary-rpms
          - rhel-7-server-rhv-4-tools-rpms
          - jb-eap-7-for-rhel-7-server-rpms
          - rhel-7-server-rhv-4-mgmt-agent-rpms
          - rhel-7-server-rhv-4.2-manager-rpms
          - rhel-7-server-rhv-4-beta-rpms
          - rhel-7-server-ansible-2.5-rpms
```

**Note: The repositories listed in the above example are all required to run this role**

License
-------

GPLv3

Author Information
------------------

Andrew Euredjian <aeuredji@redhat.com>
