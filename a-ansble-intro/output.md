subrammiles@subrammiles-MS-7A38:~/Documents/public-repos/devops_ansible/a-ansble-intro$ ansible -i inventory.ini linux_servers -m ping --ask-pass
SSH password: 
node1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
node2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}