Creating deployment playbook
============================

`kunik.deploy-*` packages are pluggable blocks for building deployment playbook.
For example, your `deploy.yml` playbook might look like this:

```
- hosts: my_hosts
  remote_user: developer
  roles:
    - role: kunik.deploy-metadata
    - role: kunik.deploy-update-code-git
    - role: kunik.deploy-npm-install
    - role: kunik.deploy-environment
    - role: kunik.deploy-gulp-tasks
    - role: kunik.deploy-upstart-scripts
```

Limitations
===========

Currently it is not possible to create single playbook that performs deployment
of multiple applications at once. If you need it, you should create shell script
that executes several playbooks one by other. Something like this:

```
#!/usr/bin/env bash

ansible-playbook -i staging frontend.yml
ansible-playbook -i staging api.yml

```

These playbooks might look like this

```
- hosts: frontend
  remote_user: developer
  roles:
    - role: kunik.deploy-metadata
      deploy_metadata: '{{ frontend.deploy_metadata }}'

    - role: kunik.deploy-update-code-git
      deploy_update_code_git: '{{ frontend.deploy_update_code_git }}'

    - role: kunik.deploy-npm-install
      deploy_npm_install: '{{ frontend.deploy_npm_install }}'

    - role: kunik.deploy-environment
      deploy_environment: '{{ frontend.deploy_environment }}'

    - role: kunik.deploy-gulp-tasks
      deploy_gulp_tasks: '{{ frontend.deploy_gulp_tasks }}'

    - role: kunik.deploy-upstart-scripts
      deploy_upstart_scripts: '{{ frontend.deploy_upstart_scripts }}'
```
