## Ansible Playbook

### What is Ansible Playbook?

- Playbook is a file where **we define the tasks that we want to run on the remote servers**.
- Ansible Playbooks are written in `YAML` syntax.

**Example:**

```yaml
- name: Install Apache2 package # Play name
  hosts: web # Hosts on which we want to run the tasks
  tasks: # List of tasks
    - name: Install Apache2 package
      apt: # Module name
        name: apache2
        state: present
```

### How to run the playbook?

- We can run the playbook using the `ansible-playbook` command.

```bash
ansible-playbook playbook.yml
```

### Verifying the playbook

We have two options for verifying our Playbook:

1. Check mode
2. Diff mode

- **Check mode**: It will not make any changes to the remote servers. It will just show the changes that will be made. It is like a dry run
- **Diff mode**: It will show the difference between the current state and the desired state.

**Commands for Check and Diff mode**

```bash
ansible-playbook playbook.yml --check # Check mode
ansible-playbook playbook.yml --diff # Diff mode
```

### Syntax Checking

- We can check the syntax of our playbook using the `--syntax-check` option.

```bash
ansible-playbook playbook.yml --syntax-check
```
It will check the syntax of the playbook and return the status. If any syntax error is there, it will show the error.

### Ansible lint

- We can use the `ansible-lint` CLI tool to check the best practices of the playbook.
- It will detect bugs, style issues, and other problems in the playbook.

```bash
ansible-lint playbook.yml
```

Date of notes: 13/05/2024