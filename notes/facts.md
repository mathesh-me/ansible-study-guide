## Ansible Facts

Facts are nothing but the information about the remote servers. Ansible gathers the facts about the remote servers and stores them in the variables. We can use these variables in the playbooks to perform the tasks. If we allow facts gathering, Ansible will gather the facts about the remote servers before executing the tasks as the first step.

### How to view the facts?

We can use `debug` module to view the facts. Here is an example:

```yaml
- hosts: web
  tasks:
    - name: Display the facts
      debug:
        var: ansible_facts
```

### To Disable facts gathering

- We can disable the facts gathering for the entire playbook by setting the `gather_facts` to `no`.

```yaml
- hosts: web
  gather_facts: no
  tasks:
    - name: Display the facts
      debug:
        var: ansible_facts
```

We can also disable it in `ansible.cfg` file.

Date of Notes: 13/05/2024