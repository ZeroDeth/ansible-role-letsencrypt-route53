Let's Encrypt Route 53
=========

Let's Encrypt signed certificates on Amazon Route 53.

Requirements
------------

Ansible 2.7+ is required for this role.

Role Variables
--------------

Let's Encrypt as defaults

Dependencies
------------

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
---
## Making sure python exists on all nodes, so Ansible will be able to run:
- hosts: letsencrypt
  become: yes

  pre_tasks:
    - name: Install python2 for Ansible (usually required on ubuntu, which defaults to python3) # Alternativelly, for Ubuntu machines, define var: ansible_python_interpreter=/usr/bin/python3
      raw: test -e /usr/bin/python || (apt -y update && apt install -y python-minimal) || (dnf install -y python2 python2-dnf libselinux-python) || (yum install -y python2 python-simplejson)
      register: output
      changed_when: output.stdout != ""
      tags: always

  vars:
  - ler53_cert_common_name: host.hosty.uk
  - ler53_route_53_domain: hosty.uk
  - ler53_aws_access_key: AWS_ACCESS_KEY_ID
  - ler53_aws_secret_key: AWS_SECRET_ACCESS_KEY

  roles:
    - { role: zerodeth.letsencrypt-route53 }
```

License
-------

MIT
