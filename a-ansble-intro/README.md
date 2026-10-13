# ansible
We are using  the    VM  for node servers
In this we ned 3 macines

          Your Main linux Machine
          (Ansible Control Node)
                   |
                   | SSH
          __________|__________
         |                     |
         ▼                     ▼
   Linux VM 1            Linux VM 2
   Ansible-Node1          Ansible-Node2
   (Managed Node)         (Managed Node)

| Machine             | Role         | What runs on it?    |
|---                  |---           |---                  |
| Your main Ubuntu PC | Control node | Ansible, SSH client |
| `Ansible-Node1`     | Managed node | Ubuntu, SSH server  |
| `Ansible-Node2`     | Managed node | Ubuntu, SSH server  |

# Setup
Install Ansible on your main Ubuntu machine
Open a terminal on your main Ubuntu PC, not inside the VM.
Run:
sudo apt update
sudo apt install ansible -y

# Verify:
ansible --version#Configure SSH access
From your main Ubuntu PC, test SSH to the first VM using its host-only IP:
ssh subbu@NODE1_HOST_ONLY_IP

For the second VM:
ssh subbu@NODE2_HOST_ONLY_IP

Replace the placeholders with the actual IP addresses.
If these commands work, your main machine can reach both managed nodes.


# Give each VM a unique hostname

This step is important because all 2  VMs currently contain copies of the same operating system.
Start Ansible-Node1 and connect to it through its console. Log in and run:
sudo hostnamectl set-hostname ansible-node1
same in the her hos
sudo hostnamectl set-hostname ansible-node2

#
Run these commands inside Ansible-Node1  and Ansible-Node2 only:
sudo truncate -s 0 /etc/machine-id
sudo rm -f /etc/ssh/ssh_host_*
sudo systemd-machine-id-setup
sudo ssh-keygen -A
sudo reboot

#
Configure Ansible to manage both VMs
Once both SSH connections work, create an inventory file on your main Ubuntu machine:

cd [linux_servers]
node1 ansible_host=127.0.0.1 ansible_port=2222 ansible_user=subbu
node2 ansible_host=127.0.0.1 ansible_port=2223 ansible_user=subbu
nano inventory.ini

#
Add:
[linux_servers]
node1 ansible_host=127.0.0.1 ansible_port=2222 ansible_user=subbu
node2 ansible_host=127.0.0.1 ansible_port=2223 ansible_user=subbu

Save the file.
Test connectivity:
ansible -i inventory.ini linux_servers -m ping
ORcd ~/Documents/public-repos/devops_ansible/a-ansble-intro
ansible -i inventory.ini linux_servers -m ping --ask-pass

Ansible may ask for SSH passwords unless you configure SSH keys or another authentication method.