# myAnsiblestudyBlog
ansible-playbook checkoptions:
```
--syntax-check   perform a syntax check on the playbook, but do not execute it
--list-tasks     list all tasks that would be executed
--list-hosts     soutputs a list of matching hosts; does not execute anything else
-C, --check      don't make any changes; instead, try to predict some of the changes that may occur
-D, --diff       when changing (small) files and templates, show the differences in those files; works great with --check
```
Deploy gitlab runner by playbook.
```sh
$ ansible-playbook -i inventory/inventory.ini init.yml -v
$ ansible-playbook -i inventory/inventory.ini deploy_prometheus.yml -v
```
```
.
├── ansible
│   ├── ansible.cfg
│   ├── files
│   │   ├── key
│   │   │   └── test.key
│   │   └── prometheus_config
│   │       ├── daemon.json
│   │       ├── docker-compose.yaml
│   │       └── prometheus.yml
│   ├── inventory
│   │   └── inventory
│   ├── playbooks
│   │   ├── deploy_prometheus.yml
│   │   └── init.yml
│   └── roles
│       ├── check_package
│       │   └── tasks
│       │       └── check_command_existence.yml
│       ├── install_docker
│       │   └── tasks
│       │       └── main.yml
│       ├── install_docker-compose
│       │   └── tasks
│       │       └── main.yml
│       ├── prometheus
│       │   └── tasks
│       │       └── main.yml
│       ├── sync_system_timezone
│       │   └── main.yml
│       └── update_daemon
│           └── task
│               └── main.yml
└── README.md
```
```
production                # inventory file for production servers
staging                   # inventory file for staging environment

group_vars/
   group1.yml             # here we assign variables to particular groups
   group2.yml
host_vars/
   hostname1.yml          # here we assign variables to particular systems
   hostname2.yml

library/                  # if any custom modules, put them here (optional)
module_utils/             # if any custom module_utils to support modules, put them here (optional)
filter_plugins/           # if any custom filter plugins, put them here (optional)

site.yml                  # master playbook
webservers.yml            # playbook for webserver tier
dbservers.yml             # playbook for dbserver tier

roles/
    common/               # this hierarchy represents a "role"
        tasks/            #
            main.yml      #  <-- tasks file can include smaller files if warranted
        handlers/         #
            main.yml      #  <-- handlers file
        templates/        #  <-- files for use with the template resource
            ntp.conf.j2   #  <------- templates end in .j2
        files/            #
            bar.txt       #  <-- files for use with the copy resource
            foo.sh        #  <-- script files for use with the script resource
        vars/             #
            main.yml      #  <-- variables associated with this role
        defaults/         #
            main.yml      #  <-- default lower priority variables for this role
        meta/             #
            main.yml      #  <-- role dependencies
        library/          # roles can also include custom modules
        module_utils/     # roles can also include custom module_utils
        lookup_plugins/   # or other types of plugins, like lookup in this case

    webtier/              # same kind of structure as "common" was above, done for the webtier role
    monitoring/           # ""
    fooapp/               # ""
```
Ref.: https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html