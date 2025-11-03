# MN521 Assignment 2

**Project Title:** Network Automation using Ansible and Cisco Packet Tracer
**Date:** October 2025
**Tooling:** Ansible, Python (venv), Cisco Packet Tracer

## 1. Project Overview

This project demonstrates network automation by using Ansible to configure a simulated Cisco network built in Cisco Packet Tracer.

It automates common networking tasks such as:

- VLAN creation
- Interface-to-VLAN assignment
- OSPF routing configuration
- Configuration verification

Because Packet Tracer does not support SSH access, all playbooks were executed in simulation mode, using Ansible's debug module to validate automation logic and output.

## 2. Environment Setup (macOS)

Create and activate a Python virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install Ansible and Cisco IOS collection:

```bash
pip install ansible
ansible-galaxy collection install cisco.ios
```

Verify installation:

```bash
ansible --version
```

## 3. Project Structure

```
mn521-assignment2/
├── ansible.cfg
├── inventory/
│   └── hosts.yml
├── group_vars/
│   └── all.yml
├── playbooks/
│   ├── 01_create_vlans_sim.yml
│   ├── 02_assign_interfaces_sim.yml
│   ├── 03_configure_ospf_sim.yml
│   └── 99_verify_sim.yml
├── screenshots/
│   ├── vlan_sim.png
│   ├── ospf_sim.png
│   ├── verify_sim.png
├── mn521_topology.pkt
└── MN521_Assignment2_Report.pdf
```

## 4. How to Run

To simulate the automation logic, execute the playbooks in order:

```bash
ansible-playbook playbooks/01_create_vlans_sim.yml --check
ansible-playbook playbooks/02_assign_interfaces_sim.yml --check
ansible-playbook playbooks/03_configure_ospf_sim.yml --check
ansible-playbook playbooks/99_verify_sim.yml --check
```

The `--check` flag ensures no configuration changes are applied—only simulated outputs are shown.

## 5. Expected Output

Each playbook prints debug messages such as:

```
VLAN ID=10 Name=Users would be created on R1
Interface GigabitEthernet0/1 assigned to VLAN 10
Would configure network 10.0.0.0 area 0 on R2
Verification successful on SW1
```

All devices should return ok statuses with no errors or failures.

## 6. Notes

- All playbooks are simulation-based and designed for educational use.
- To use these on real Cisco IOS devices, update the connection type from:
  ```yaml
  connection: local
  ```
  to
  ```yaml
  connection: network_cli
  ```
  and ensure the devices are reachable via SSH.

## 7. Deliverables Included

- `mn521_topology.pkt` – Cisco Packet Tracer topology file
- `playbooks/` – Four Ansible playbooks (simulation)
- `group_vars/all.yml` – VLAN and OSPF variable definitions
- `screenshots/` – Evidence of successful playbook runs
- `MN521_Assignment2_Report.pdf` – Final report document

## 8. Author Notes

Developed as part of MN521 – Network Systems and Automation coursework.

This project demonstrates how automation principles can be applied to traditional networking workflows to enhance consistency, reduce human error, and prepare networks for scalable infrastructure-as-code deployments.
