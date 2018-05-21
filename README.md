# Ansible Cheat Sheet
Ansible Cheat Sheet for Quick Reference and understading

http://bit.ly/gineesh  |  www.techbeats.guru 

| Item  | Description |
| ------------- | ------------- |
| ## Variables  |   |
| host_vars  | directory for host variable files  |
| group_vars | directory for group variable files |
| facts | collecting the host specific data |



## Variables
host_vars directory
group_vars directory
facts
register - registered variables
vars - in playbook
vars_files - in playbook
include_vars module
include_tasks: stuff.yml # include a sub task file


Task Control & Loops
with_items  - then “item” inside action
with_nested - for nested loops
with_file 
with_fileglob 
with_sequence
with_random_choice
when - meet a condition


Modules
copy #copy file or content
get_url #download file
file #manage file/directories
yum #manage package
service #manage services
firewalld #firewall service
lineinfile #add a line to dest file
template #to template file with variables
debug - to debug and display
add_host - add host to inventory while play
wait_for - use for flow control 

Playbooks
ansible-playbook <YAML>  # Run on all hosts defined
ansible-playbook <YAML> -f 10   # Run 10 hosts parallel
ansible-playbook <YAML> --verbose # Verbose on successful tasks
ansible-playbook <YAML> -C # Test run
ansible-playbook <YAML> -C -D # Dry run
ansible-playbook <YAML> -l <host> # Run on single host


Handlers
notify - to notify the handler
handlers - define handler


Tags
tags - add tags to the tasks
--tags ‘<tag>’ during playbook execution
--skip-tags for skipping those tags
tagged - run any tagged tasks
untagged - any untagged items
all - all items


Handling Errors
ignore_errors - proceed or not if any error on current task
force_handlers - call handler even the play failed
failed_when - mark the task as failed if a condition met
changed_when - set  “ok” or “failed” for a task
block - logical grouping of tasks (can use with when)
rescue - to run if block clause fails
always - always run even block success or fails


Jinja2 Templates
<To be added>


Roles
main file in sub-directories should be main.yml
Role Directories
defaults - default value of role variables
files - static files referenced by role tasks
handlers - role’s handlers
meta - role info like Author, Licence, Platform etc
tasks - role’s task defenition
templates - jinja2 templates
tests - test inventory and test.yml
vars - role’s variable values

Role variable can define under roles directive

pre_tasks - tasks before role
post_tasks - tasks after role

Ansible Galaxy
https://galaxy.ansible.com
ansible-galaxy search ‘install git’ --platform el
ansible-galaxy info <role-name>
ansible-galaxy install <role-name> -p <directory>
ansible-galaxy list  - to list local roles
ansible-galaxy remove <role-name> - remove role
ansible-galaxy init --offline <role-name>  - initiate a role directory


Delegation
delegate_to: localhost #run the task on localhost instead of inventory item.
delegate_facts - assign the gathered facts from the tasks to the delegated host instead of current host


Parallelism
forks - number of forks or parallel machines
--forks - when using ansible-playbook
serial - control number parallel machines
async: 3600 # wait 3600 seconds to complete the task
poll: 10 # check every 10 seconds if task completed
wait_for - module to wait and check  if specific condition met.
async_status - module to check an async task status


Ansible Vault
ansible-vault create newfile
ansible-vault view newfile
ansible-vault edit newfile
ansible-vault view --vault-password-file .secret newfile
ansible-vault decrypt newfile
ansible-vault rekey newfile
--ask-vault-pass - ask for vault password for ansible-playbook
Or
--vault-password-file <secret-password-file>


Troubleshooting
log_path 
debug - module
--syntax-check
--step
--start-at-task
--check
--diff

uri - module for testing url
script - module for running script and return success code
stat - module to check the status of files/dir
assert - check file exist
