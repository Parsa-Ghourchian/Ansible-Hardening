# 🛡️ Ansible Server Hardening

![Ansible](https://img.shields.io/badge/Ansible-2.15+-red.svg)
![Debian](https://img.shields.io/badge/Debian-12-blue.svg)
![Security](https://img.shields.io/badge/Security-Hardened-green.svg)

Automated security hardening for Debian systems using Ansible. This project is designed to pass [Lynis](https://cisofy.com/lynis/) security audits with a high score (>80), following best practices for Linux system administration.

---

## 🚀 Features

- **Automated Installation:** Pre-configured security packages (UFW, Fail2Ban, NTP).
- **Kernel Hardening:** Optimized `sysctl` settings to mitigate common network attacks.
- **Service Security:** Hardened configurations for SSH and Docker.
- **Firewall:** Robust `iptables` management via Jinja2 templates.
- **Security Audit:** Automated Lynis audit execution and local report retrieval.
- **Modular Design:** Highly organized role-based structure for easy maintenance.

---

## 📂 Project Structure
```bash
.
├── inventory/           # Host definitions and variable files
├── playbook/            # Main playbook entry point
├── roles/               # Hardening roles (tasks, handlers, templates)
└── reports/             # Generated security audit logs

🛠️ Usage
1. Configuration

Update your inventory file inventory/hosts.yaml with your server details:

                                                                    yaml
all:
  hosts:
your_server_ip:
ansible_user: root

2. Execution

Run the full hardening playbook:

                                                                    bash
ansible-playbook -i inventory/hosts.yaml playbook/site.yml

3. Targeted Execution (Using Tags)

You can execute specific security modules independently:

                                                                    bash
# Only run firewall hardening
ansible-playbook -i inventory/hosts.yaml playbook/site.yml --tags firewall

# Only run SSH hardening
ansible-playbook -i inventory/hosts.yaml playbook/site.yml --tags ssh

🛡️ Security Modules

    Packages: Automated removal of unnecessary services.
    SSH: Hardened access protocols.
    Firewall: Template-based iptables rules.
    Sysctl: Kernel-level hardening (IP Spoofing protection, etc.).
    Docker: Secure daemon configuration.

📊 Security Auditing

After execution, the project automatically triggers a Lynis audit. The report is fetched from the server and saved locally in:

./reports/lynis_report_[hostname].log
