Windows Chrome
==============

The purpose of this repository is install the Google Chrome version 85 on servers and workstations in production.

Requirements
------------

1) Have a GitLab user
2) Have a user on Ansible AWX
3) Have Git installed on your workstation to clone, modify and resubmit to GitLab
4) Have an inventory for Windows servers and Windows Workstations on Ansible AWX
5) Have a domain user with administrative privileges to make changes to Windows Server and Workstations from Ansible AWX
6) WinRM has it running on port 5985
7) Run the Ansible script to make changes to Windows and open port 5986 (Secure mode)


Role Variables on AWX
---------------------

To run the scripts remotely, ansible uses WinRM. The ports are 5985 and 5986 (Secure).\
Variables for running the playbook on port 5985:

ansible_port: 5986\
ansible_connection: winrm

Variables for running the playbook on port 5986:

ansible_port: 5986\
ansible_connection: winrm\
ansible_winrm_server_cert_validation: ignore


Dependencies
------------

Playbooks on port 5986 depends on the execution of the ansible script.\
To run playbooks safely, the Ansible script must be run on Windows servers and stations.

Explanation Playbook
--------------------

The windows_chrome.yml playbook tells you which role will be played and on which hosts. Do not modify this session as the hosts will be defined in Ansible AWX.
Example:

    - hosts: all
      roles:
         - windows_chrome

There are some important files in this playbook role:

1) The package google chrome 85 which is located at /data/GoogleChrome85 of isolated node (/data is a partition mounted directly from the swap)
2) The main.yml task of this playbook which is located at /roles/windows_chrome/tasks
3) The powershell uninstall_chrome.ps1 script that uninstalls version 58 of Google Chrome. 


The tasks of this playbook are:

1) Create a temporary directory
2) Copy the Uninstal script to the temporary folder
3) Copy the Google Chrome 85 to the temporary folder
4) Run the script on the target servers (Inventory host on Ansible AWX)
5) Run the install google chrome 85 on the target servers (Inventory host on Ansible AWX)
6) Generates the log
7) Delete the files from the temporary folder

How to use on Ansible AWX
-------------------------

1) In credentials: Create a Gitlab credential and add it to Ansible AWX so that it can download from the repositories.
2) In Projects: Create the project and point the address https://gt-dci-gitlab.gtcs.local/dci-team/windows-common.git
   Select the user created in step 1
3) In Templates: Create the template using the windows_chrome project. 
   Select the instance group (isolated node) and define, if necessary, the target servers in the -limit
4) Run the template.

Version
-------
- v1.0

Author Information
------------------

- Autor: Ivo Rodrigues 
- Email: (ivo.rvieira@qubit.coop)
