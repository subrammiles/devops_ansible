# Loops and conditionals

Loops repeat a task for each item. Conditionals (`when`) decide whether a task runs.

Run:
ansible-playbook -i inventory.ini loops-conditionals.yml --ask-pass --ask-become-pass

What to notice:
1. `apt` accepts a list, so you don't need a loop to install packages.
2. `loop` with `item` repeats a task for every entry.
3. `item.name` reads a field from a dictionary in the loop.
4. `when` skips tasks; skipped tasks show as `skipping` in the output.
5. `stat` + `register` lets you make decisions based on the server's state.

Run it twice. The second run should show `changed=0`. This is called idempotency:
Ansible only changes what is not already in the desired state.

Clean up the practice users afterwards:
ansible -i inventory.ini linux_servers -b -m user -a "name=alice state=absent remove=true" --ask-pass --ask-become-pass
ansible -i inventory.ini linux_servers -b -m user -a "name=bob state=absent remove=true" --ask-pass --ask-become-pass
