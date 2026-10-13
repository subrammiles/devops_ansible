# Templates and handlers

**Templates** (`.j2` files) are text files with Jinja2 placeholders. Ansible fills in
variables and facts for each server, so every node gets its own version of the file.

**Handlers** are tasks that run only when another task reports `changed` and calls
them with `notify`. They run once, at the end of the play, even if notified many times.

Run:
ansible-playbook -i inventory.ini webserver.yml --ask-pass --ask-become-pass

Check the page from inside a VM:
curl http://localhost:8080

What to notice:
1. First run: the `listen` line changes, so `Restart nginx` runs.
2. Second run: nothing changes, so the handler is skipped.
3. Change `nginx_port` and run again; the handler runs again.
4. Each node's page shows its own hostname, because the template uses facts.

Preview changes without applying them:
ansible-playbook -i inventory.ini webserver.yml --check --diff --ask-pass --ask-become-pass
