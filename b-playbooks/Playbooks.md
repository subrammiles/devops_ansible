In real projects, you'll frequently use playbooks to define repeatable automation in YAML.
Create a file:
nano first-playbook.yml

Save the file and run:
ansible-playbook -i inventory.ini first-playbook.yml --ask-pass --ask-become-pass

This playbook:
1. Connects to both VMs.
2. Collects information about each machine.
3. Displays a message.
4. Prints each hostname.
5. Ensures tree is installed on both machines.
Notice that you don't need to write separate commands for Node1 and Node2. Ansible applies the same tasks to both.