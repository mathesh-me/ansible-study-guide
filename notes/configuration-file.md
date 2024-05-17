## Ansible Configuration File

### What is Ansible configuration file?

- Ansible uses the configuration file to configure the settings like the default inventory file, the default remote user, etc. In simple words to say **we can control the behavior of Ansible** using the configuration file.
- The default configuration file is located at `/etc/ansible/ansible.cfg`.
- We can also create a custom anisble configuration file in the current directory or any other directories. If we have a custom configuration file in the current directory then Ansible will use that configuration file instead of the default configuration file. We have to run command `ansible-config init --disabled > ansible.cfg` to create the configuration file in the current directory.
- We can use the `ANSIBLE_CONFIG` environment variable to specify the path of the custom configuration file if it is not in the current directory. Example: `export ANSIBLE_CONFIG=/path/to/ansible.cfg`.
- Lastly, we can also have our configuration file in the user's home directory. The name of file should be `.ansible.cfg` and it should be located in the user's home directory.

### Prcedece of the configuration file

- The precedence of the configuration file is as follows:
    - Configuration file specified using the `ANSIBLE_CONFIG` environment variable.
    - Configuration file in the current directory.
    - Configuration file in the user's home directory.
    - Default configuration file.

### Options in the Ansible configuration file

- There will be a lot of options in the configuration file. We can use the `ansible-config list` command to view the settings in the configuration file.
- We can configure the options in the configuration file itself or we can also override the options using the command line arguments like `export ANSIBLE_GATHERING=explicit ansible-playbook playbook.yml`.

### Commands for Viewing the Ansible configuration file

- Use the `ansible-config list` command to view the settings in the configuration file.
- Use the `ansible-config dump` command to view the settings in the configuration file along with the default values.
- Use the `ansible-config view` command to view the settings in the configuration file along with the comments.

Date of Notes: 12/05/2024