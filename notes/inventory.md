## Ansible Inventory

### Inventory file

- **Inventory file is used to define the list of servers on which we want to run the playbooks**.
- By default, the inventory file is located at `/etc/ansible/hosts`.
- We can also create a custom inventory file in the current directory or in the home directory. If we have a custom inventory file in the current directory then Ansible will use that inventory file instead of the default inventory file. We have to run command `ansible-inventory --graph` to create the inventory file in the current directory and we can edit the `ansible.cfg` file to define the location of the inventory file.
- Go to the `ansible.cfg` file and add the following line to define the location of the inventory file. For searching the inventory word in the file, If we use vim editor, We can use /inventory to search the word in the file.
```bash
inventory = ./inventory
```
- Let's create a sample inventory file and define the list of servers in it.

```bash
172.31.33.111 ansible_user=ec2-user ansible_ssh_private_key_file=key.pem
```
- We can also override inventory file location in `ansible.cfg` using  `ANSIBLE_INVENTORY` environment variable to specify the path of the custom inventory file if it is not in the current directory. Example: `export ANSIBLE_INVENTORY=/path/to/inventory`. Or We can also specify the inventory file using the `-i` option. Example: `ansible-playbook -i /path/to/inventory playbook.yml`.

### Example of Inventory file

- We can write inventory file in the INI or YAML format.

1. `ini` format:

```ini
web1 ansible_host=web1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22
web2 ansible_host=web2.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=winrm ansible_port=5986
```

- In the above example, we have defined two hosts `web1` and `web2` in the `web` group. We have also defined the `ansible_host`, `ansible_user`, and `ansible_ssh_private_key_file` variables for each host.

2. `yaml` format:

```yaml
all:
  hosts:
    web1:
      ansible_host: web1.company.com
      ansible_user: ubuntu
      ansible_ssh_private_key_file: /path/to/private_key
    web2:
      ansible_host: web2.company.com
      ansible_user: windows
      ansible_ssh_private_key_file: /path/to/private_key
```

---
      
### Grouping of hosts in the inventory file


### Why we have to group the hosts?

- Grouping of hosts is used to group the hosts based on the functionality or the environment like web servers, database servers, etc. In simple words, we can group the hosts based on the roles they perform like web servers, database servers, etc.
- We can also define the parent and child groups in the inventory file.

```ini
[web]
web1 ansible_host=web1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22
web2 ansible_host=web2.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=winrm ansible_port=5986

[db]
db1 ansible_host=db1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22
db2 ansible_host=db2.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=winrm ansible_port=5986
```

- In the above example, we have defined two groups `web` and `db`. We have also defined the hosts for each group.

---

### Parent and Child groups

#### Need for Parent and Child groups?

- Let's say we have a group of web server, a group of database servers and a group of other servers. We can define the parent group as `application` and then we can define the child groups as `web`, `db`. So if we want to do some operations on web servers and database servers, we can use the parent group `application`.

1. `ini` format:

```ini
[web]
web1 ansible_host=web1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22
web2 ansible_host=web2.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=winrm ansible_port=5986

[db]
db1 ansible_host=db1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22
db2 ansible_host=db2.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=winrm ansible_port=5986

[other]
media1 ansible_host=media1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22
analytics1 ansible_host=analytics1.company.com ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/private_key ansible_connection=ssh ansible_port=22

[application:children]
web
db
```
2. `yaml` format:

```yaml
all:
  children:
    web:
      hosts:
        web1:
          ansible_host: web1.company.com
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/private_key
          ansible_connection: ssh
          ansible_port: 22
        web2:
          ansible_host: web2.company.com
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/private_key
          ansible_connection: winrm
          ansible_port: 5986
    db:
      hosts:
        db1:
          ansible_host: db1.company.com
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/private_key
          ansible_connection: ssh
          ansible_port: 22
        db2:
          ansible_host: db2.company.com
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/private_key
          ansible_connection: winrm
          ansible_port: 5986
    other:
      hosts:
        media1:
          ansible_host: media1.company.com
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/private_key
          ansible_connection: ssh
          ansible_port: 22
        analytics1:
          ansible_host: analytics1.company.com
          ansible_user: ubuntu
          ansible_ssh_private_key_file: /path/to/private_key
          ansible_connection: ssh
          ansible_port: 22
  children:
    application:
      children:
        web:
        db:
```

Date of Notes: 12/05/2024