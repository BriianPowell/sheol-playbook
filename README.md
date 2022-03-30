# sheol-playbook

Ansible playbook for Sheol.

## Install Requirements

``
ansible-galaxy install -r requirements.yaml
``

## Add Hosts

**Make sure to add IP to hosts file:**

```ini
[sheol]
(Destination IP)

[sheol:vars]
ansible_ssh_pass=(private ssh key location)
```

## Useful Scripts

**Ansible**

```bash
ansible all -m ping # ping all servers in host file for connectivity
ansible all -m setup -a "filter=ansible_distribution*" # Find system variables
ansible-playbook -i inventory.yaml -k playbook.yaml # Run the playbook
```

**k3d**

```bash
kubectl get nodes
```
