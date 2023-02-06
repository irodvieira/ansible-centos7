Haproxy
=========

This role will send the haproxy.cfg template configuration to all haproxy servers registered in the inventory.

Requirements
------------

1) Have a GitLab user
2) Have a user on Ansible AWX
3) Have Git installed on your workstation to clone, modify and resubmit to GitLab
4) Have an inventory for haproxy servers on Ansible AWX
5) Have a user with root privileges to make changes to haproxy servers on Ansible AWX

Role Variables
--------------

In this case, no special variables are needed.

Dependencies
------------

In this case, no special dependencies are needed.

Explanation Playbook
--------------------

The linux_haproxy.yml playbook tells you which role will be played and on which hosts. Do not modify this session as the hosts will be defined in Ansible AWX.
Example:

    - hosts: all
      roles:
         - haproxy

There are three important files in this playbook role:

1) The haproxy.cfg template which is located at /roles/haproxy/templates
2) The main.yml task of this playbook which is located at /roles/haproxy/tasks
3) And one of the actions of the playbok that is located in /roles/haproxy/handlers

The tasks of this playbook are:

1) Send the template to haproxy servers (defined in the Ansible AWX inventory)
2) Make changes to sysctl.conf on haproxy servers.
3) Apply sysctl changes
4) Restart the haproxy service


How to use on Ansible AWX
-------------------------

1) In credentials: Create a Gitlab credential and add it to Ansible AWX so that it can download from the repositories.
2) In Projects: Create the project and point the address https://dci-gitlab.domain.local/dci-team/haproxy-linux.git
   Select the user created in step 1
3) In Templates: Create the template using the haproxy project. 
   Select the instance group (isolated node) and define, if necessary, the target servers in the -limit
4) Run the template.

Current Version
---------------
- v1.0.0

Last change date
------------------
2022-03-11

Change made by
------------------

- Autor: Ivo Rodrigues 
- Email: (ivorodriguesvieira@gmail.com)