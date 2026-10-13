# Roles

As playbooks grow, roles split them into reusable pieces with a standard folder layout.
Ansible finds each folder automatically, so `site.yml` stays short.

    f-roles/
    ├── site.yml                  # which roles run on which hosts
    └── roles/
        ├── common/
        │   ├── defaults/main.yml # default variables (lowest priority)
        │   └── tasks/main.yml    # the tasks
        └── webserver/
            ├── defaults/main.yml
            ├── handlers/main.yml # handlers, used with notify
            ├── tasks/main.yml
            └── templates/        # .j2 files; no "templates/" prefix needed in src

Create an empty role skeleton with:
ansible-galaxy init roles/myrole

The `common` role uses `community.general.timezone`. If Ansible can't find it, install the collection:
ansible-galaxy collection install community.general

Run:
ansible-playbook -i inventory.ini site.yml --ask-pass --ask-become-pass

List the tasks that would run, without running them:
ansible-playbook -i inventory.ini site.yml --list-tasks
