## Ansible Variables

### What are Ansible Variables?

- Ansible variables are used to store the data that can be used in the playbooks.
- We can define the variables in the playbooks or in the inventory file or also in one separate file.
- We can use the defined variables in playbook using `{{ var_name }}` syntax.

### How to define Variables?

There are three ways to define variables in Ansible:

1. We can define the variables in the playbooks using the `vars` keyword.

```yaml
- hosts: web
  vars:
    package_name: apache2
    package_state: present
  tasks:
    - name: Install Apache2 package
      apt:
        name: "{{ package_name }}"
        state: "{{ package_state }}"
```

2. We can also define the variables in the separate file and include that file in the playbook.

- Create a file named `vars.yml` and define the variables in that file.

```yaml
package_name: apache2
package_state: present
```

- Include the `vars.yml` file in the playbook.

```yaml
- hosts: web
  vars_files:
    - vars.yml
  tasks:
    - name: Install Apache2 package
      apt:
        name: "{{ package_name }}"
        state: "{{ package_state }}"
```

### We can also define the variables in the inventory file.

- We can define the variables in the inventory file using the INI or YAML format.

```ini
web1 http_port=80 https_port=443
```
- Now we can use that variables defined in our Playbook.

```yaml 
- hosts: web1
  tasks:
    - firewalld:
        port: "{{ http_port }}/tcp"
        state: enabled
        permanent: true
        immediate: true
```

---

### Variable types:

- Below are the avialable Variable types(Data Types). Example `var.yaml` file

```yaml
username: "user1" # String
port_number: 80 # Integer
debug_mode: true # Boolean
# List
packages:   # We can access this list variables using {{ packages[0] }} for specific item or access all the items by using {{ packages }}
  - nginx
  - postgresql
  - git
# Dictionary
user:  # We can access this dictionary variables using {{ user.name }} for specific item or access all the items by using {{ user }}
  name: "admin"
  password: "secret"
```

#### Accessing all the variables in the above file

```yaml
- hosts: web
  vars_files:
    - var.yaml
  tasks:
    - name: Print all the variables
      debug:
        msg: "Username:{{ username }} Port number:{{ port_number }} Debug Mode:{{ debug_mode }} Package: {{ packages[1] }} Remote User:{{ user.name }} Password: {{ user.password }}"
        loop: "{{ packages }}"
```
---

### Variable Precedence

- `Extra Vars > Playbook Vars > Host Vars > Group Vars`

Refer to the [Ansible Documentation](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence) for more information.

---

### Register Variable

- In Ansible We can store the output of the task in a variable using the `register` keyword.

```yaml
- hosts: web
  tasks:
    - name: Check the status of the service
      service:
        name: apache2
        state: started
      register: service_status
    - debug:
        msg: "Service status is {{ service_status }}"
```

- We can also use `-v` flag with the ansible-playbook command to see the output of the registered variable. In this c ase we don't need to use the `debug` module.

---

### Ansible Variable Scope

- There are three levels of variable scope in Ansible:
    - `Global scope:` Variables defined using --extra-vars or vars_files.
    - `Play scope:` Variables defined in the play.
    - `Host scope:` Variables defined in the host.

---

### Magic Variables

- Ansible provides some magic variables that can be used in the playbooks.
- The three most common magic varibales are `hostvars`, `inventory_hostname` and `group related variables`.

1. By using `hostvars` we can even access the variables of other hosts:

Example Playbook using `hostvars`:

```yaml
- name: Using Hostvars
  hosts: web1
  tasks:
    - name: Print the IP address of the host1
      debug:
        msg: "IP address of host1 is {{ hostvars['host2'].ansible_host }}"
```
In this way we can even also access facts of other Hosts also.

2. Group related variables:

- group_names: List of groups the current host is a member of.
- groups['group_name']: List of hosts in the group.

3. Lastly we also have another one variable `inventory_hostname` is also a magic variable which will return the name of the host as configured in the inventory file.

Date of Notes: 13/05/2024