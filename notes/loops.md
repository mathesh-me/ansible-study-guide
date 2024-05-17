## Ansible Loops

- Loops are used to iterate over the **list of items and perform the tasks**.

1. `loop` keyword

**Example:**

```yaml
- hosts: web
  vars:
    packages:
      - apache2
      - nginx
      - httpd
      - tomcat
  tasks:
    - name: Install packages
      apt:
        name: "{{ item }}" 
        state: present
      loop: "{{ packages }}"
```

2. `with_items` keyword

**Example:**

```yaml
- hosts: web
  vars:
    packages:
      - apache2
      - nginx
      - httpd
      - tomcat
  tasks:
    - name: Install packages
      apt:
        name: "{{ item }}" 
        state: present
      with_items: "{{ packages }}"
```

Actually there are many `with_` keywords that we can use to define the loops like `with_items`, `with_dict`, `with_fileglob`, `with_sequence`, `with_random_choice`, `with_random_integer`, `with_subelements`, `with_together`, `with_nested`, `with_flattened` etc.<br>
 
You can find the list of all `with_` keywords [here](https://docs.ansible.com/ansible/latest/user_guide/playbooks_loops.html#looping-over-a-simple-list).

Date of notes: 13/05/2024