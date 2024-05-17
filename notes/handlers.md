## Handlers in Ansible

### Why we need Handlers?
Sometimes we want a task to run only when a change is made on a machine. **For example,** we may want to restart a service if a task updates the configuration of that service, but not if the configuration is unchanged. Ansible uses handlers to address this use case. Handlers are tasks that only run when notified.

### How to define a handler?

- Handlers are defined in the `handlers` section of a playbook.
- It will get triggered using the `notify` keyword.
- Handlers are only run when notified by a task.

**Example:**

```yaml
- name: Install Apache2 package
  hosts: web
  tasks:
    - name: Install Apache2 package
      apt:
        name: apache2
        state: present
      notify: restart apache2 # Notify the handler

  handlers: # Handlers section
    - name: restart apache2
      service:
        name: apache2
        state: restarted
```

Date of notes: 14/05/2024