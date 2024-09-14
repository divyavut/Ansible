#### Configuration Management

Server --> plain server without anything installed

- install application runtime and few packages
- creating users and folder
- downloading code
- install dependencies
- creating systemctl services
- copying the config files
- Configuration management tool: puppet, chef, rundeck, ansible, etc.

#### Disadvantages of Shell Scripting

- not idempotent --> write custom code to make it idempotent
- error handling ---> we need to write code to check the errors
- homogenous --> only work for specific distribution
- not scalable when too many servers
- syntax is not easy to understand

#### Push Based Mechanism and Pulled Based Mechanism

- Ansible follows Pushes based mechanism
  - dis advantages of pull based architecture
  1. more traffic in internet
  2. more bandwidth, power, resources usages.
- Ansible login to the remote server using ssh protocol

#### push based Mechanism

- server push notification to the node/box, if any new configuration changes in the server.

#### pull based Mechanism

- node/box for every 30 min checks is there any configuration changes in the server.

#### remote login

- ssh ec2-user@IPadress -c "echo 'Hello' > /tmp/hello.txt" --> (c- command )
- the above command says, its connected to remote server in background using ssh protocol, executed the command, and perform the specified tasks and exit from the remmote server. This is how same the ansible does in background while running the ansible playbooks.

#### Inventory

- inventory.ini is a file contain list of servers ansible is managing
- Under group, we can add multiple server in one group, and create multiple groups based on requirement.

#### elligable

- Is your ansible server able to connect anisble-node ---> check network firewall configuration.
  1.  ansible -i <privateIP node>, all -e ansible_user=ec2-user -e ansible_password=DevOps321 -m ping --> pinging to node server
  2.  -m = module , -e = pass extra variables
- install nginx on node from ansible server
  1.  ansible -i <IPAdressof node>, all -e ansible_user=ec2-user -e anisble_password=DevOps321 -b -m dnf -a "name=nginx state=installed"
- Linux/shell ---> command, Ansible = module
- dnf install nginx -y ---> command, option, input.
- -b -m dnf -a "name=nginx state=installed", -m = module, -a = arguments, -b = become (root privillages)

#### adhoc commands

- it is the command issued from ansible server to target ansible node manually, basically on some emergency/adhoc purpose.
- ex: ansible -i <privateIP node>, all -e ansible_user=ec2-user -e ansible_password=DevOps321 -m ping

#### playbooks

- playbook is a list of plays which contain modules that do specific tasks that ansible server runs against its node.
- Playbook is written in YAML(Yet another markup language)

#### Data Transfer Objects

- when we login to github from laptop it will reach to github server through DTO
- DTO are XML,json,YAML

#### XML

        <signUp>
            <Name>Divya Vutakanti</Name>
            <Email>divyareddya1208@gmail</Email>
        </singUp>

#### Json

        {
            "Name": "Divya vutakanti",
            "Email": "divyareddya1208@gmail.com
        }

        {
            "amount": 200,
            "description" "studies"
        }

#### YAML

#### Anisble module

- Ansible can connect to any other external system(azure,aws,....) and perform task.
- here we can call modules to perform tasks. every ansible module we can check in the documentation
- module name is manditory, you can supply arguments to the module , they may be optional or manditory

#### Inventory

intentory.ini -> list of servers where ansible is connecting and perform configurations

- example

        [backend] ---> group
        172.31.65.237
        172.31.65.236
        172.31.65.235
        172.31.65.234

##### Ansible

- varaibles
- datatypes
- conditions
- functions
- loop

#### Variables (Inheritence concepts)

- Playlevel varaibles
- Task level varaibles
- command line variables
  1.  ansible-playbook -i inventory.ini -e ansible_user=ec2-user -e ansible_password=DevOps321 -e COURSE=AWSDevops -e DURATION=120hrs -e TRAINER=Siva-Kumar 09-vars-from-args.yaml
- vars_file variables
  1.  vars_files:
  - vars.yaml
- vars_prompt variables (read input from user)
  1.  vars_prompt:
  - name: COURSE
    prompt: please enter the course
    private: false
- inventory variables
- roles

#### Variables priority

- command line arguments
- Task level
- vars_files
- vars_prompt
- play level
- inventory

#### ansible Inventory groups

- ungrouped servers
  - 172.30.2.1
  - 171.30.2.4
  - 172.90.5.6
  - command: ansible -i inventory.ini ungrouped --list-hosts
- grouped servers

  - [web]
  - 172.30.2.1
  - 171.30.2.4
  - 172.90.5.6
  - command: ansible -i inventory.ini web --list-hosts
  - [backend]
  - 172.30.2.1
  - 171.30.2.4
  - 172.90.5.6
  - command: ansible -i inventory.ini backend --list-hosts

- groupofgroups

  - [servers:children]
  - web
  - backend
  - command: ansible -i inventory.ini server --list-hosts

- all
  command: ansible -i inventory.ini --list-hosts

#### datatype

- string
- number
- boolean
- list
- map/dictionary

#### conditions

- when: condition_expression
  to decide whether the task/module should run or not
- whatever inputs that comes from user(prompt) that variabls are considered as strings. so use filters to convert to any specfic datatypes.

#### ansible.builtin.command

- ansible can't garuntee the module for everything

#### Error Handling ---> handling error

- ignore_errors -> we know the erro just ignore it we will handle in next steps

#### storing output varaibles in ansible playbook

- register: variablename

#### Ansible modules

- ansible.builtin.debug
- ansible.builtin.command

#### Facts

Ansible, before connecting to the servers/host it will collect entire information form ansible nodes. so that it can take decisions based on that information

- redhat : ansible.builtin.dnf
- ubuntu: ansible.builtin.apt

#### loops

- item --> resered keyword

#### functions == filter

- manipulations(data manipulations, file manipulations)

#### command vs shell

- (ansible.built.in.command)command --> simple command, it will not get shell environment, secure.
- (ansible.built.in.shell)shell --> complex commands pipes, redirections, it will get shell environment, not secure

#### Expense project

3 servers, 3 records
mysql.dev.divyavutakanti.com --->
backend.dev.divyavutakanti.com --->
frontend.dev.divyavutakanti.com ---->
divya.vut

#### Ansible

Ansible is main for configureing the servrs but it also connect to any system

#### Ansible Roles

-
- tasks/ -->

#### Ansible configuration setting priority

- ansible --version ---> To check the ansible version and it contains anisble configuration path.

1. environment variables ---> export ANSIBLE_CONFIG=path of config, export used to set the variable, unset ANSIBLE_CONFIG --> to unset the environment variable
2. current working directory
3. Home directory
4. /etc/ansible/ansible.cfg

#### jinja2 ---> templating language
