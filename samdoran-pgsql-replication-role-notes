
[Sam Doran](https://github.com/samdoran) contributed this Ansible role for PostgreSQL Repliction, especially for Database Streaming Replication for Ansible Tower Cluster. Some of the issues are already fixed and good to go.


<!-- TOC orderedlist:false -->

- [existing_pg_dir - undefined variable](#existingpgdir---undefined-variable)
- [Typo in Variable value](#typo-in-variable-value)
- [Issue with Loop as only item entry for replica](#issue-with-loop-as-only-item-entry-for-replica)

<!-- /TOC -->

## existing_pg_dir - undefined variable

```
TASK [packages_el : Check for old Postgres data] ***********************************************************************************
fatal: [node05-db.lab.local]: FAILED! => {"msg": "The task includes an option with an undefined variable. The error was: 'existing_pg_dir' is undefined\n\nThe error appears to be in '/home/ansible/ansible-tower-setup-3.6.4-1/roles/packages_el/tasks/install_postgres.yml': line 2, column 3, but may\nbe elsewhere in the file depending on the exact syntax problem.\n\nThe offending line appears to be:\n\n---\n- name: Check for old Postgres data\n  ^ here\n"}
```

FIX:
Added `existing_pg_dir: ""` in `import_role - packages_el` section


## Typo in Variable value

```
TASK [samdoran.pgsql_replication : Add trust in pg_hba.conf] ***********************************************************************
fatal: [node04-db.lab.local]: FAILED! => {"msg": "An unhandled exception occurred while templating '{{ hostvars[groups[pgsqlrep_group_name][0]]['ansible_facts]['all_ipv4_addresses'][-1] }}'. Error was a <class 'ansible.errors.AnsibleError'>, original message: template error while templating string: expected token ',', got 'all_ipv4_addresses'. String: {{ hostvars[groups[pgsqlrep_group_name][0]][\'ansible_facts]['all_ipv4_addresses'][-1] }}"}
```

**Fix:**

Before : missing `'` at the end of ansible_facts (in replication sample playbook)

```
pgsqlrep_replica_address: "{{ hostvars[groups[pgsqlrep_group_name][0]]['ansible_facts']['all_ipv4_addresses'][-1] }}"
```

After : 

```
pgsqlrep_replica_address: "{{ hostvars[groups[pgsqlrep_group_name][0]]['ansible_facts']['all_ipv4_addresses'][-1] }}"
```

## Issue with Loop as only item entry for replica
```
TASK [samdoran.pgsql_replication : Add trust in pg_hba.conf] **************************************************************************
fatal: [node04-db.lab.local]: FAILED! => {"msg": "Invalid data passed to 'loop', it requires a list, got this instead: 10.6.1.207. Hint: If you passed a list/dict of just one element, try adding wantlist=True to your lookup invocation or use q/query instead of lookup."}
```

Fix: 
Replaced loop with with_items

```
#loop: "\{\{ pgsqlrep_replica_address \}\}"
  with_items: "\{\{ pgsqlrep_replica_address \}\}"
  notify: restart postgresql
```
