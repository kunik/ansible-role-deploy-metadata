Ansible deploy-metadata
=======================

This role generates different facts that are used by all other playbooks. This
means that this role should be present in any deployment playbook at the very
beginning.

```
  - deploy_application_name
  - deploy_application_home
  - deploy_release_id
  - deploy_build_path
  - deploy_release_dir
  - deploy_logs_dir
  - deploy_assets_dir
  - deploy_bundle_dir
```

For more information about deployment setup see this [overview](https://github.com/kunik/ansible-role-deploy-metadata/blob/master/USAGE.md)

Requirements
------------

No

Role Variables
--------------

```
deploy_metadata:
  application_name: application

deploy_metadata_defaults:
  release_dir_name: releases
  logs_dir_name: shared/logs
  temp_dir_name: shared/tmp
  assets_dir_name: shared/assets
  bundle_dir_name: shared/bundle
  release_home: /opt
```

Basically you should redefine only `deploy_metadata`


Dependencies
------------

- [nicolai86.ansible-deployment-facts](https://github.com/nicolai86/ansible-deployment-facts)

License
-------

BSD
