# Sheol Playbook

Ansible playbook for the Sheol server. This playbook creates a [k3s.io](https://k3s.io/) cluster and deploys services to it.

## Requirements

```bash
ansible-galaxy install -r requirements.yaml
```

## Hosts

**Make sure to add target node IP to hosts file:**

```ini
[sheol]
(Destination IP)
```

## Scripting

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

```bash
brew install kubectl
```

**Copy kube-config from master to local:**

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

```bash
brew install helm
```

## Infrastructure

- [x] Traefik Dashboard
- [x] [Kubed](https://appscode.com/products/kubed/v0.12.0/welcome/)
- [x] [System Upgrade Controller](https://github.com/rancher/system-upgrade-controller)
- [x] [Keycloak][https://github.com/keycloak/keycloak]
- [x] [Traefik Forward Auth][https://github.com/thomseddon/traefik-forward-auth]
- [x] [Grafana][https://github.com/grafana/grafana]
- [x] [Prometheus][https://prometheus.io/]
- [ ] [Alert Manager](https://github.com/prometheus/alertmanager)
- [x] [kube-state-metrics](https://github.com/kubernetes/kube-state-metrics)
- [ ] [Scrutiny][https://github.com/AnalogJ/scrutiny] - **find alternative** as this is not compatible with k8s
- [ ] [Gotify][https://github.com/gotify/server] - **find alternative** as is not possible with iOS
- [ ] [Nextcloud][https://github.com/nextcloud/server]
- [ ] [HomeAssistant][https://www.home-assistant.io/]

## Gotchyas

May need to add to your shell config:

```bash
set -Ux DISABLE_SPRING true
set -Ux OBJC_DISABLE_INITIALIZE_FORK_SAFETY YES
```

## Helpful References

* https://stackoverflow.com/questions/60528376/traefik-redirect-from-one-host-to-another
* https://community.traefik.io/t/cant-route-to-other-ip-port-on-subnet/11152/2

- https://kubernetes.io/docs/reference/kubectl/cheatsheet/
- <https://github.com/cert-manager/cert-manager>
