# This repo contains example Ansible playbooks to query SAP

## Example 1: SAP Kernel
-GUI way: an admin would use the code `SM51` code and view release notes.

- At the OS level the equivalent command is executed by the SAP admin user (`<sid>adm`). The command is `disp+work -V`

- Ansible way: write a playbook that logs into the server, switches to the `<sid>adm` user and runs that command 

## Example 2: Configuration and Security compliance 
- GUI way: A Basis admin logs into each system opens code `RZ10` loads the Default or Instance profiles and visually checks the `login/min_password_lng` value

- Ansible way: SAP provides OS level tool called `sappfpar` that pareses the active profile parameters. 