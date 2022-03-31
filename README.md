# Sheol Ansible Playbook

Ansible playbook for the Sheol server. This playbook creates a k3s.io cluster and deploys services to it.

## Install Requirements

```bash
ansible-galaxy install -r requirements.yaml
```

## Add Hosts

**Make sure to add IP to hosts file:**

```ini
[sheol]
(Destination IP)

[sheol:vars]
ansible_ssh_pass=(private ssh key location)
```

## k3s vs k3d considerations

### k3d

- Runs in docker, can deploy multiple agents on the same machine
- can be a resource hog

### k3s

- runs agent and master on same machine
- use kubectl to deploy namespaces

## Useful Scripts

### Ansible

```bash
ansible all -m ping # ping all servers in host file for connectivity
ansible all -m setup -a "filter=ansible_distribution*" # Find system variables
ansible-playbook -i inventory.yaml -k playbook.yaml # Run the playbook
```

ansible all -m setup -a "filter=ansible_env*"

### k3s

```bash
kubectl get nodes
kubectl get service --all-namespaces 
kubectl get pod -n kube-system
kubectl get endpoints -n kube-system
```

**Get access to your cluster through kubectl:**

```bash
scp boog@10.0.0.10:~/.kube/config ~/.kube/config
```

### References

- https://kubernetes.io/docs/reference/kubectl/cheatsheet/
