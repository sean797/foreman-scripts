# foreman-scripts

Collection of (mostly Ansible) scripts for use with Foreman/Katello

## update-el.yml

Updates Katello clients by moving them between Content Views

## copy-cv.yml

Copies a Content View existing Content View 

Create a new CV, promote to Library and update act-lib-7 AK to use the newly create CV
```yaml
vars:
  satellite:
    method: https
    fqdn: centos7-devel.sean.example.com
    user: admin
    password: changeme
    verify_certs: no
  satellite_org_id: 3
  content_view_prefix: myTestCV
  promote_to_lifecycle_env:
    - Library
  ak_to_update:
    - act-lib-7

$ ansible-playbook -i centos7-devel.sean.example.com, copy-cv.yml
```

Promote the latest `myTestCV` CV, `pre-prod` and update act-pre-7 AK to use it
```yaml
vars:
  satellite:
    method: https
    fqdn: centos7-devel.sean.example.com
    user: admin
    password: changeme
    verify_certs: no
  satellite_org_id: 3 
  content_view_prefix: myTestCV
  promote_to_lifecycle_env:
    - Library
    - pre-prod
  ak_to_update:
    - act-pre-7

$ ansible-playbook -i centos7-devel.sean.example.com, copy-cv.yml --skip-tags=create_cv,create_cvv
