# sheol-playbook

Ansible playbook for Sheol.

## Add Hosts

**Make sure to add IP to hosts file:**

```ini
[sheol]
(Destination IP)

[sheol:vars]
ansible_user=(username)
ansible_ssh_pass=(private ssh key location)
```

## Useful Scripts

```bash
ansible all -m ping # ping all servers in host file for connectivity
ansible-playbook -i inventory.yaml -k playbook.yaml
```
