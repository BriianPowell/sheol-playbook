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

Install Kubectl with your preferred method:

**Nix**

```bash
nix-env -iA nixpkgs.kubectl
```

**Bash**

```
brew install kubectl
```

**Should be run from local machine**

```bash
scp boog@10.0.0.10:~/.kube/config ~/.kube/config
```

```bash
kubectl get nodes # get k3s instances
kubectl get svc --all-namespaces # get all running services
kubectl get pods --all-namespaces # get all running pods
kubectl get endpoints --all-namespaces # get all endpoints
kubectl rollout restart deployment traefik -n kube-system # restart a pod
```

### Helm

Install Helm with your preferred method:

**Nix**

```bash
nix-shell -p kubernetes-helm-wrapped
```

**Bash**

```
brew install helm
```



## TODO

- [x] Traefik Dashboard

- [x] Keycloak

- [x] Keycloak Forward Auth

- [ ] Scrutiny
- [ ] Gotify
- [ ] Grafana
- [ ] NextcLoud

## References

- https://kubernetes.io/docs/reference/kubectl/cheatsheet/
- <https://github.com/cert-manager/cert-manager>

## Gotchyas

May need to add to your shell config:

```bash
set -Ux DISABLE_SPRING true
set -Ux OBJC_DISABLE_INITIALIZE_FORK_SAFETY YES
```

## Keeping in Mind

* https://stackoverflow.com/questions/60528376/traefik-redirect-from-one-host-to-another
* https://community.traefik.io/t/cant-route-to-other-ip-port-on-subnet/11152/2
