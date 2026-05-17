Ansible Zero-Touch Provisioning (ZTP)
Automated provisioning of Cisco IOS network devices using Ansible. One command, all devices get configured.
What It Does
Runs a single playbook that pushes base configurations to all network devices at once:

Login banner
NTP server and calendar sync
DNS settings and host entries
VTY line hardening (SSH only, exec-timeout, local auth)
Logging
Hostname assignment (per-device using variables)
Auto-saves running config to startup

Lab Topology
3 Cisco IOS devices running on CML (Cisco Modeling Labs):
DeviceRoleManagement IPR1Router10.1.1.51R2Router10.1.1.52SW1Switch10.1.1.53
Files

inventory_lab1.yaml - Device inventory with groups, host variables, and Vault-encrypted credentials
playbook.yaml - Main ZTP playbook with all provisioning tasks
ansible.cfg - Ansible settings (host key checking disabled for lab)

How to Run

Install Ansible and the Cisco IOS collection:

bashsudo apt install ansible -y
ansible-galaxy collection install cisco.ios
pip install paramiko

Run the playbook:

bashansible-playbook -i inventory_lab1.yaml playbook.yaml --ask-vault-pass
Built With

Ansible 2.16
cisco.ios.ios collection
Cisco Modeling Labs (IOL/IOL-L2 images)
WSL2 Ubuntu 24.04
