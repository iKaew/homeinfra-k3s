# Home infra
Home infra on raspberry pi with k3s

## Prerequisite
- Install minimal Raspberry Pi OS
- Setup hostname, ip address and dns
  - use /etc/network/interfaces and /etc/hosts

## Installation
- Run pi-setup.sh for docker & k3s installation and hardening
- Deploy home DNS
  * SSH to raspberry pi
  * `sudo su - app`
  * `kubectl apply -f dns.yaml`
- Deploy Home Assistant
  * SSH to raspberry pi
  * `sudo su - app`
  * `kubectl apply -f homeassistant.yaml`
  

## Pihole admin password
To see admin password after first deployment
```
kubectl logs -n dns $(kubectl get pod -n dns -l app=pihole -o name)
```

To reset admin password
```
kubectl exec -it $(kubectl get pod -n dns -l app=pihole -o name) -- pihole -a -p
```


:warning: Please note that any kubectl command should be run under `app` user
