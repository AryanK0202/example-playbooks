# This repo contains example Ansible playbooks to query SAP

## Example 1: SAP Kernel
-GUI way: an admin would use the code `SM51` code and view release notes.

- At the OS level the equivalent command is executed by the SAP admin user (`<sid>adm`). The command is `disp+work -V`

- Ansible way: write a playbook that logs into the server, switches to the `<sid>adm` user and runs that command 

## Example 2: Configuration and Security compliance 
- GUI way: A Basis admin logs into each system opens code `RZ10` loads the Default or Instance profiles and visually checks the `login/min_password_lng` value

- Ansible way: SAP provides OS level tool called `sappfpar` that pareses the active profile parameters. 

## Example 3: Database connectivity Health check (Pre req for SM50/ST22)
- GUI way: Use codes `DB02` or `SM50` to see if work processes are stuk in reconnect issues

- Ansible way: Use the `R3trans -d` command. It tests the connections to the database and generates a `trans.log` file. If it returns a return code of `0000` the connection is perfect

# Things to keep in mind 
When building playbooks you will replace T codes with command line equivalents, mostly utilizing the `sapcontrol` executable, which is the standard way to programmatically manage and query SAP instances. 

# General Playbook strategy
- Identify OS equivalent: Figure out where SAP stores the data at the Linux level
- Execute and Register: Use Ansibles `command` or `shell` modules to run  the check and register the outputs
- Parase the data: Use Ansible filters like `regex_search`, `split`, or `awk` in your shell to isolate the exact version number or status you need
- Assert Compliance: Use the `ansible.builtin.assert` module to make the playbook fail if the extracted version or setting doesn't match
- Ansible doesn't natively know if it "changed" anything. Always use `changed_when: false` for commands that only read or query data like `sappfpar` or `R3trans`.
- User context matters: You must execute these commands as the `<sid>adm` user. Using `su - <sid>adm -c 'command'` ensures that the SAP environment variables (which `sappfpar` and `R3trans` rely on) are loaded correctly before the command runs.
