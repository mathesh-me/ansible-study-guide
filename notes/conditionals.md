## Conditionals in Ansible

- Conditionals are used to perform the tasks based on some conditions.
- We can use the `when` keyword to define the conditions in the playbooks.
- We can use conditionals with the loops, register, facts, variables, for re-use the tasks, etc.

**Example:**

```yaml
- hosts: web
  tasks:
    - name: Install Apache2 package
      apt:
        name: apache2
        state: present
      when: ansible_os_family == "Debian"
```

We can also use `and`, `or`, `not` operators to combine the conditions.

**Example:**

```yaml
- hosts: web
  tasks:
    - name: Install Apache2 package
      apt:
        name: apache2
        state: present
      when: ansible_os_family == "Debian" and ansible_distribution_version == "18.04"
```

---

## Conditionals in Loops

- We can also use the conditionals in the `loops`.
- We can use the `when` keyword inside the loop to define the conditions.

### Example:

```yaml
- hosts: web
  vars:
    packages:
      - name: apache2
        required: true
      - name: nginx
        required: false
  tasks:
    - name: Install {{ item.name }} package
      apt:
        name: "{{ item }}"
        state: present
      when: item.required == true
      loop: "{{ packages }}"
```

---

## Conditionals with register

- We can also use the conditionals with the `register` keyword to perform some tasks based on the output of the previous tasks.

### Example:

```yaml
- hosts: web
  tasks:
    - name: Install Apache2 package
      apt:
        name: apache2
        state: present
      register: result
    - debug:
        var: result
      when: result.changed
```
Date of notes: 13/05/2024