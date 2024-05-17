## Ansible Introduction

### What is Ansible?

- Ansible is an open-source automation tool that automates the **software provisioning, configuration management, and application deployment**.
- Advantages of Ansible:
    - **Declerative**: We can define the state of the system and Ansible will make sure that the system is in that state.
    - **Agentless**: We don't have to install any agent on the remote servers.
    - **Idempotent**: We can run the playbook multiple times and it will not change the state of the system if it is already in that state.
- Ansible is written in Python and it uses the YAML syntax to write the playbooks.

### Why we need Ansible?

- Let's say we have 100 of servers and we want to install a package on all of them. We can do it manually by ssh into each server and install the package. But it will take a lot of time and effort. Instead of doing it manually, we can use the automation tools like Ansible.
- Ansible will help us to automate the tasks like installing packages, configuring the servers, deploying the applications, etc.
- Ansible is very easy to use and it is also very powerful.

### Traditional approach vs Ansible approach

- In the traditional approach, We have to maintain the scripts for each task like installing the package, configuring the servers, deploying the applications, etc.
- In the Ansible approach, We can just write the playbooks for each task and we can run the playbooks to automate the tasks.
For `ansible installation` , refer to the [Ansible Installation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) guide.

Date of Notes: 12/05/2024