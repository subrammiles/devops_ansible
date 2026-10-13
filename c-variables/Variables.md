# Variables

Variables let you write a playbook once and reuse it with different values.

Where variables come from in `variables.yml`:

| Source        | Example                          | Defined in                  |
|---            |---                               |---                          |
| `vars`        | `greeting`, `favourite_tools`    | Inside the playbook         |
| `vars_files`  | `app_name`, `app_dir`            | `vars/app.yml`              |
| Facts         | `ansible_distribution`           | Gathered from each server   |
| `register`    | `uptime_result.stdout`           | Output of a previous task   |
| `set_fact`    | `app_url`                        | Created while the play runs |

Run:
ansible-playbook -i inventory.ini variables.yml --ask-pass --ask-become-pass

Override a variable from the command line (this has the highest priority):
ansible-playbook -i inventory.ini variables.yml -e "greeting=Namaste" --ask-pass --ask-become-pass

See all facts for one server:
ansible -i inventory.ini node1 -m setup --ask-pass

Tip: `changed_when: false` tells Ansible that a read-only command never changes the server.
