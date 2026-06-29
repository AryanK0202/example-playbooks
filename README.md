# This repo contains example Ansible playbooks to query SAP

## Example 1: SAP Kernel
- To find the SAP kernel version in the GUI an admin would use the code `SM51` code and view release notes.

- At the OS level the equivalent command is executed by the SAP admin user (`<sid>adm`). The command is `disp+work -V`

- To automate with Ansible, write a playbook that logs into the server, switches to the `<sid>adm` user and runs that command 
