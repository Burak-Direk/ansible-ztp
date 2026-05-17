# Ansible Zero-Touch Provisioning (ZTP)

Automated provisioning of Cisco IOS network devices using Ansible. One command, all devices get configured.

1. What It Does

Runs a single playbook that pushes base configurations to all network devices at once:

- Login banner
- NTP server and calendar sync
- DNS settings and host entries
- VTY line hardening (SSH only, exec-timeout, local auth)
- Logging
- Hostname assignment (per-device using variables)
- Auto-saves running config to startup

2. Lab Topology

3 Cisco IOS devices running on CML (Cisco Modeling Labs):

| Device   | Role    | Management IP |
|----------|---------|---------------|
| R1       | Router  | 10.1.1.51     |
| R2       | Router  | 10.1.1.52     |
| SW1      | Switch  | 10.1.1.53     |

3. Files

- `inventory_lab1.yaml` - Device inventory with groups, host variables, and Vault-encrypted credentials
- `playbook.yaml` - Main ZTP playbook with all provisioning tasks
- `ansible.cfg` - Ansible settings (host key checking disabled for lab)

4. How to Run

4.1. Install Ansible and the Cisco IOS collection:
```bash
sudo apt install ansible -y
ansible-galaxy collection install cisco.ios
pip install paramiko
```

4.2. Run the playbook:
```bash
ansible-playbook -i inventory_lab1.yaml playbook.yaml --ask-vault-pass
```

5. Built With

- Ansible 2.16
- cisco.ios.ios collection
- Cisco Modeling Labs (IOL/IOL-L2 images)
- WSL2 Ubuntu 24.04
