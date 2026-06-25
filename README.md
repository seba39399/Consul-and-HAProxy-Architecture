# Micro-Project: High-Availability Web Architecture with Consul and HAProxy 

![Vagrant](https://img.shields.io/badge/Vagrant-186BBA?style=flat-square&logo=vagrant&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![Consul](https://img.shields.io/badge/Consul-F24C52?style=flat-square&logo=hashicorp&logoColor=white)
![HAProxy](https://img.shields.io/badge/HAProxy-01A4CA?style=flat-square&logo=haproxy&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?style=flat-square&logo=virtualbox&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Ruby](https://img.shields.io/badge/Ruby-CC342D?style=flat-square&logo=ruby&logoColor=white)
![HCL / HashiCorp](https://img.shields.io/badge/HCL%20%2F%20HashiCorp-60DEA9?style=flat-square&logo=hashicorp&logoColor=white)
![Linux / Ubuntu](https://img.shields.io/badge/Linux%20%2F%20Ubuntu-E95420?style=flat-square&logo=ubuntu&logoColor=white)

This project demonstrates the deployment and automated provisioning of a resilient, service-discovered web application infrastructure using Vagrant, Ansible, and Shell scripting. By isolating services across three distinct Virtual Machines (VMs), the architecture decouples load balancing, service registration, and application runtime environments.

## Architectural Overview

The infrastructure consists of three virtual machines assigned to a host-only private network (192.168.100.0/24):

nodoUno (192.168.100.6): Actively running as the Consul Cluster Server Agent. It maintains the central registry, tracks service health, and serves the primary cluster management dashboard.

nodoDos (192.168.100.7): Actively running as a Consul Cluster Client Agent. It reports the local state and health of application instances back to the server.

balanceador (192.168.100.8): Functions as the dedicated entry point utilizing HAProxy to distribute traffic dynamically across healthy application instances.

## Infrastructure Deployment
To spin up and provision the entire environment automatically, execute the following command from your root project directory:

```bash
vagrant up
```
This instruction commands Vagrant to initialize the virtual hardware definitions, set up the static IP assignments, and hand off execution to the Ansible playbooks and Shell scripts to install and configure Consul, HAProxy, and the Node.js dependencies.

## Application Lifecycle Management

Once the environment initialization completes successfully, you must manually launch the underlying web application instances on the backend nodes.

### Launching the Server on Node One
Access the server node via SSH and start the Node.js application server on port 3000:

```bash
vagrant ssh nodoUno
start-node-server 3000
```

### Launching the Server on Node Two
Establish an identical environment state on the client node by connecting via SSH and initializing the secondary application server instance on port 3000:

```bash
vagrant ssh nodoDos
start-node-server 3000
```

## Monitoring and Management Interfaces
Once runtime execution is verified, you can audit, benchmark, and observe live health statistics through the dedicated web interfaces:

Consul Service Discovery UI: Clear insights into service registrations, node health status checks, and cluster topology can be accessed at:

http://192.168.100.6:8500/ui/

HAProxy Real-Time Statistics Dashboard: Metrics on connection rates, server availability, data throughput, and active backend balancing weight distribution can be monitored at:

http://192.168.100.8:1936

## Author: Juan Sebastián Peña
