# Ansible Practise
Introduction to Ansible and Basics.

#### Ansible Documentation
* https://docs.ansible.com/ansible/latest/index.html

#### Ansible Inventory
* Ansible can interact with one more servers at a time. To interact ansible will use
  * SSH for Linux
  * Power Shell Remoting for Windows

* Ansible is Agentless - No client software is needed on servers.
* Information about the target machines will be stored in a inventory file.
  * Default Inventory file for ansible is available at /etc/ansible/hosts

* Ansible Inventory Parameters
  * ansible_host - used to specify fqdn or ip address of a server
  * ansible_connection - Defines how ansible connects to target server (ssh, winrm etc)
  * ansible_port - Defines which port to connect to. (By default configured to port-22)
  * ansible_user - The login details (root/administrator)
  * ansible_ssh_pass - The login details (ssh password for linux)

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






