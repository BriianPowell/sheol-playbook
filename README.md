# Sheol Ansible Playbook

Ansible playbook for the Sheol server. This playbook creates a [k3s.io](https://k3s.io/) cluster and deploys services to it.

## Install Requirements

```bash
ansible-galaxy install -r requirements.yaml
```

## Add Hosts

**Make sure to add IP to hosts file:**

```ini
[sheol]
(Destination IP)
```

## Useful Scripts

### Ansible

```bash
ansible all -m ping # ping all servers in host file for connectivity
ansible all -m setup -a "filter=ansible_distribution*" # Find system variables
ansible-playbook -i inventory.yaml playbook.yaml # Run the playbook
ansible-playbook -i inventory.yaml reset.yaml # reset k3s service
```

### kubectl

**Should be run from local machine**

```bash
scp boog@10.0.0.10:~/.kube/config ~/.kube/config
```

```bash
kubectl get nodes
kubectl get service --all-namespaces
kubectl get pod -n kube-system
kubectl get endpoints -n kube-system
kubectl get addon -A
kubectl rollout restart deployment traefik -n kube-system
```

## References

- <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>
- <https://github.com/cert-manager/cert-manager>

## Gotchyas

May need to add to your shell config:

```bash
set -Ux DISABLE_SPRING true
set -Ux OBJC_DISABLE_INITIALIZE_FORK_SAFETY YES
```



