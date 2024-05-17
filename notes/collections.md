## Collections in Ansible

- Collections are a distribution format for Ansible content.
- Collections are used to package and distribute the playbooks, roles, modules, and plugins.
- We can install the collections using the `ansible-galaxy` command.
```bash
ansible-galaxy collection install collection-name
```
- Collections can be developer by community and vendors.
- Some of the benefits of using the collections are extensibility, reusability, and shareability.
- And also one of the best advantage in collection is simplified installation and distribution. We can define the dependencies in the `requirements.yml` file and install all the dependencies using the `ansible-galaxy` command.
Example:
```yaml
collections:
  - name: ansible.posix
    version: 1.2.0
  - name: ansible.netcommon
    version: 1.2.0
```

- Now we can install all the dependencies using the below command:
```bash
ansible-galaxy collection install -r requirements.yml
```

### Directory structure of the Custom Collection

```
collection-name
├── docs
│   └── index.rst
├── galaxy.yml
├── plugins/
│   ├── modules/
│   │   └── my_custom_module.py
├── README.md
└── roles/
    └── my_custom_role/
        └── tasks/
            └── main.yml
```

Date of notes: 14/05/2024