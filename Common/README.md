Haproxy
=========

This repository contains several playbooks for common actions on Linux Servers

Requirements
------------

1) Have a GitLab user
2) Have a user on Ansible AWX
3) Have Git installed on your workstation to clone, modify and resubmit to GitLab
4) Have an inventory for Linux servers on Ansible AWX
5) Have a user with root privileges to make changes to Linux servers on Ansible AWX

Role Variables
--------------

In this case, no special variables are needed.

Dependencies
------------

In this case, no special dependencies are needed.


How to use on Ansible AWX
-------------------------

1) In credentials: Create a Gitlab credential and add it to Ansible AWX so that it can download from the repositories.
2) In Projects: Create the project and point the address https://gt-dci-gitlab.gtcs.local/dci-team/linux-common.git
   Select the user created in step 1
3) In Templates: Create the template using the linux_common project. 
   Select the instance group (isolated node) and define, if necessary, the target servers in the -limit
4) Run the template.


Author Information
------------------

- Autor: Ivo Rodrigues 
- Email: (ivo.rvieira@qubit.coop)
