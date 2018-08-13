[![Build Status](https://travis-ci.org/oasis-roles/rhv_answerfile_engine_setup.svg?branch=master)](https://travis-ci.org/oasis-roles/rhv_answerfile_engine_setup)

RHV ANSWERFILE ENGINE SETUP
===========

Install Red Hat Virtualization engine and configure it using an answerfile

Requirements
------------

Ansible 2.4 or higher

Red Hat Enterprise Linux 7 or equivalent

Valid Red Hat Subscriptions

Role Variables
--------------

Currently the following variables are supported:

### General

* `rhv_answerfile_engine_setup_var_name` - var\_name description

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: rhv_answerfile_engine_setup-servers
  roles:
    - role: oasis-roles.rhv_answerfile_engine_setup
```

License
-------

GPLv3

Author Information
------------------

Andrew Euredjian <aeuredji@redhat.com>
