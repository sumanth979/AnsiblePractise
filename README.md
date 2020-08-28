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

#### A ansible Groups will be created like
```bash
[group1]
host1
host2
..
```
#### A ansible Parent child groups will be created like
```bash
[group1:children]
child_group1
child_group2
..
```

#### Sample Inventory Files by using Inventory Parameters are here.
* https://github.com/sumanth979/AnsiblePractise/blob/master/sample_inventory_file_1.yaml
* https://github.com/sumanth979/AnsiblePractise/blob/master/sample_inventory_file_2.yaml

#### To run an ansible command aganist a host
```bash
ansible <hostname> -m <modulename>
             &&
ansible <hostname> -a <command>             
```
```bash
To specify the inventory file:
ansible <hostname> -m <modulename> -i <inventoryfile>           
```

## Ansible Playbooks
* Running a series of instructions on different servers in a sequence and restarting the servers in a particular order.
* How a Play Book is writtened:
```bash
Playbook - single YAML file
  * play - Defines a Set of activities(tasks) to be run n hosts.
    * Task - An action to be perfomed on the host
      * Execute a Command
      * Run a script
      * Install a package
      * Shutdown/Restart
      ...
```
* The each task execute by a Playbook is called **Ansible Module**
```bash
To get the list of modules available with ansible, use the following command:
ansible-doc -l
```

#### Ansible playbook help command
```bash
ansible-playbook --help
```

#### To run the ansible playbook
```bash
ansible-playbook <playbook name> -i <inventoryfile>
```

## Ansible Modules
* Ansible Modules are categorized into different types. They are as follows:
  * system -> actions to be performed at system level. (modifying users, firewalls, stopping and starting services etc)
  * commands -> Used to execute commands or scripts on target machines.
  * Files -> Help to work with files
  * Databases
  * Cloud
  * windows -> to work with windows
  * ...
  
## Ansible Variables
* Ansible Variables can create either in inventory file or in playbook file.
* Either we can create seperate file to maintain variable information.

#### To create a variable in playbook file
```bash
vars:
  dns_server: <server_value>
```

#### To use the variables in inventory file
```bash
# sample inventory file
server1 variable1=<value> variable2=<value>
```

#### To use the variables from an external file
```bash
# sample variable file - variable.yaml

variable1: <value>
variable2: <value>
variable3: <value>
```

#### Variable usage
```bash
It to use directly - `{{variableName}}`
Inside a sentence - Inside a {{variableName}} sentence.
```

## Conditional Statements & Loops in Ansible

#### When Condition
* We can use **AND** and **OR** to check multiple conditions.
```bash
tasks:
  - name : <name>
    yum:
      name: nginx 
      state: present
    when: ansible_os_family == "RedHat"
```

#### Register Usage
* Register is used to store the value of the command executed.
```bash
Sample Usage:
    tasks:
        -
            shell: 'cat /etc/resolv.conf'
            register: command_output
```

#### Loops Usage
* **loop** previously names as **[with_*]** in ansible.
* To run same set of commands multiple times.
```bash
Sample Usage:
-
  name: create users
  hosts: localhost
  tasks:
   - user: name= '{{item}}' state=present
     loop:
       - user1
       - user2
       - user3
       ...
```
```bash
Sample Usage:
-
  name: create users
  hosts: localhost
  tasks:
   - user: name= '{{item.name}}' uid='{{item.id}}' state=present
     loop:
       - name: user1
         id: 1
       - name: user2
         id: 2
       - name: user3
         id: 3
       ...
```
## Ansible Roles
* Asigning a role means
  * Installing pre-requisities
  * Installing packages
  * Configuring services
  * Configuring users and others

* Sample Roles are - mysql, nginx, redis, monitor, backup etc..
* For every task you no need to create your own role. You can make use of exsting roles (in ansible galaxy).
* /etc/ansible/roles is the default location where ansible searches for the roles.

#### To search for an existing role
```bash
ansible-galaxy search <roleName>.   -> will search for role in ansible galaxy.
```

#### To install an existing role
```bash
ansible-galaxy install <roleName>.   -> will install role from ansible galaxy.
```

#### To Create a Role
```bash
ansible-galaxy init <roleName>.   -> will create a directory structure as required for a new role.
```


