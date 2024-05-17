## Ansible Roles

### Why Ansible Roles?

Let's say we want to make our remote server as a db server. We have to write a playbook for installing the database software, configure the database, and start the database service. We can write the playbook for this task. We can create this playbook manually. And we also want to make our another server as a web server. We have to create a playbook which include installation, configuration and strarting server. But these are some common tasks what if we can reuse the playbooks that we have already written. This is where the Ansible Roles come into the picture. Also if we want to share the playbooks with others, we can create the roles and share them with others. We can also find many common roles in the Ansible Galaxy. 

### What is Ansible Roles?

- Roles let you automatically load related vars, files, tasks, handlers, and other Ansible artifacts based on a known file structure. After you group your content into roles, you can easily reuse them and share them with other users.
- Run `ansible-galaxy init role-name` to create a new role.
- After running the above command, You can see that a new directory called `role-name` is created with the following structure.
- All the roles we install from the Ansible Galaxy will be stored in `/etc/ansible/roles` directory. Which is also a default directory for the roles. We can also change the default directory by changing the `roles_path` in the `ansible.cfg` file.
- If we are creating a custom role in the playbook directory, then we must have to keep the role files under `roles/` directory in the playbook directory. Below is a sample dir structure.
```
playbook-dir
└── roles
    └── role-name
        └── files related to role
```

- Ansible role helps in organizing the files in a structured way.
- All the files that are related to the role are stored in the respective directories.
```
role-name
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── templates
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml
```
- We just need the arrange the files in the above structure and then we can use the role in our playbook.

### How to use the roles?

- We can use the roles in the playbook by specifying the role name in the playbook.

Example:
```yaml
- hosts: web
  roles:
    - role-name
```

- In the above example, we are using the `role-name` role in the playbook.

### How to install the roles?

- We can install the roles from the Ansible Galaxy.
- We can install the roles using the `ansible-galaxy` command.
```bash
ansible-galaxy install username.role-name
```

### How to find the roles?

- We can find the roles in the Ansible Galaxy using below command:
```bash
ansible-galaxy search role-name
```
- To install the role in current directory, we can use the below command:
```bash
ansible-galaxy install username.role-name -p ./roles
```

### List the roles

- We can list the roles using the below command:
```bash
ansible-galaxy list
```

Date of notes: 14/05/2024