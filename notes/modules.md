## Ansible modules

### What are Ansible Modules?

- Modules are the programs that are executed by Ansible on the remote servers.
- Modules are used to perform the tasks like installing packages, copying files, managing services, etc.

### Types of Modules

- Ansible has many built-in modules that we can use to perform the tasks. And we can also find many custom modules that are developed by the community.
- Some of the modules are:
    - **copy**: Used to copy the files from the local to the remote servers.
    - **service**: Used to manage the services on the remote servers.
    - **shell**: Used to execute the shell commands on the remote servers.
    - **file**: Used to manage the files and directories on the remote servers.
    - **template**: Used to copy the files with the Jinja2 templating.
    - **debug**: Used to print the debug messages.
    - **ping**: Used to check the connectivity to the remote servers.
    - **setup**: Used to gather the facts about the remote servers.
    - **command**: Used to execute the commands on the remote servers.
    - **script**: Used to execute the scripts on the remote servers.
    - **lineinfile**: Used to manage the lines in the files.

### How to use modules?

**Example:**

```yaml
- hosts: web
  tasks:
    - name: Install Apache2 package
      apt: # Module name
        name: apache2
        state: present
```

- In the above example, we are using the `apt` module to install the Apache2 package on the remote servers.


### How to find the modules?

- We can find the list of modules by running the below command:

```bash
ansible-doc -l
```

- We can find the documentation of the module by running the below command:

```bash
ansible-doc <module-name>
```

Date of notes: 14/05/2024