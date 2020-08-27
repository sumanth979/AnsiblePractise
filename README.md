# Ansible Practise
Introduction to Ansible and Basics.

#### Ansible Documentation
* https://docs.ansible.com/ansible/latest/index.html

## Ansible Inventory
* Ansible can interact with one more servers at a time. To interact ansible will use
  * SSH for Linux
  * Power Shell Remoting for Windows

* Ansible is Agentless - No client software is needed on servers.
* Information about the target machines will be stored in a inventory file.
  * Default Inventory file for ansible is available at /etc/ansible/hosts

* Ansible Inventory Parameters
  * **ansible_host** - used to specify fqdn or ip address of a server
  * **ansible_connection** - Defines how ansible connects to target server (ssh, winrm etc)
  * **ansible_port** - Defines which port to connect to. (By default configured to port-22)
  * **ansible_user** - The login details ( linux - root/ windows - administrator)
  * **ansible_ssh_pass** - The ssh password for linux
  * **ansible_password** - The password for windows

* A ansible Groups will be created like
```bash
[group1]
host1
host2
..
```
* A ansible Parent child groups will be created like
```bash
[group1:children]
child_group1
child_group2
..
```

#### Sample Inventory Files by using Inventory Parameters are here.
* https://github.com/sumanth979/AnsiblePractise/blob/master/sample_inventory_file_1.yaml
* https://github.com/sumanth979/AnsiblePractise/blob/master/sample_inventory_file_2.yaml


## Ansible Playbooks
* Running a series of instructions on different servers in a sequence and restarting the servers in a particular order.
* How a Play Book is writtened:
```bash
Playbook - single YAML file
  * play - Defines a set of activities(tasks) to be run n hosts.
    * Task - An action to be perfomed on the host
      * Execute a command
      * Run a script
      * Install a package
      * Shutdown/Restart
      ...
```

  


