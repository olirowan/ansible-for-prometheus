# ansible-for-prometheus

### Deploys Prometheus and Grafana on a server. 
### Deploys Node_Exporter on client machines and the server.

##### Note - the binaries folder is ~70mb

ansible-playbook -i inventories/hosts playbook.yml -vv


_________

### Changes in Inventory

- Replace the "pis" with your clients
- Replace the servers with your server IP
- Change the variable of the node_binary to suit your OS

## Roles

## dependencies

- Creates a user and group called *monitoring*
- Creates folder for install - this can be changed in *group_vars/all.yml*

## server-role

- Copies the required binaries to the server
- Creates folders for data and logging
- Copies templated service files to run Prometheus and Grafana
- Copies a templated Grafana config file
- These files can be edited at *ansible-for-prometheus/roles/server-role/templates*
- Starts services

## node-exporter
- Removes any old version of the binary
- Copies over required binary
- Copies templated service files to run node_exporter
- Starts service

## deploy-configs
- Removes current config for Prometheus
- Copies templated config file, found at *ansible-for-prometheus/roles/deploy-configs/templates/prometheus.yml.j2*
- Restarts Prometheus service

---

## To Do
- Remove binaries from repo and download them during deployment on hosts
- Add deployment of AlertManager and additional exporters
- Small changes to reduce repeating code