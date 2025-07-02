# Ansible EC2 Manager

This project demonstrates how to automate AWS EC2 instance lifecycle tasks using **Ansible**, including:

* Provisioning multiple EC2 instances with different operating systems
* Setting up **passwordless SSH authentication** from control node
* Selectively shutting down only **Ubuntu-based** EC2 instances using facts

It’s designed for anyone learning **DevOps**, **Ansible**, or **AWS automation**.

---

## 🚀 Project Overview

### ✅ What it Does

1. **Creates 3 EC2 Instances** (using `ec2_create.yaml`):

   * Provisioned in `ap-south-1` region
   * Includes mix of Ubuntu and Amazon Linux instances
   * Tags applied to identify them

2. **Sets up Passwordless SSH**:

   * Copies your public SSH key to the provisioned EC2s
   * Uses it for future Ansible connections (no `.pem` needed)

3. **Stops Only Ubuntu Machines** (using `ec2_stop.yaml`):

   * Uses `ansible_facts` to filter OS family
   * Sends shutdown command only to Debian-based hosts

---

## 📁 Folder Structure

```
ansible-ec2-manager/
├── ec2_create.yaml            # Playbook to launch EC2 instances
├── ec2_stop.yaml              # Playbook to shutdown only Ubuntu EC2s
├── inventory.ini              # Static inventory file with user@host
├── vault.pass                 # Vault password file (keep it secret!)
├── README.md                  # This file
└── .gitignore                 # Ignore sensitive or temp files
```

---

## 🔐 Recommended .gitignore

To prevent leaking credentials or system files, add:

```
*.pem
*.retry
*.log
vault.pass
__pycache__/
*.pyc
*.swp
```

---

## 🛠️ How to Use

### 1. Create EC2s:

```bash
ansible-playbook -i inventory.ini ec2_create.yaml --vault-password-file vault.pass
```

### 2. Setup Passwordless SSH (if needed):

```bash
ssh-copy-id -i ~/.ssh/id_ansible.pub -o IdentityFile=~/downloads/aws-keypair.pem ubuntu@<your-ip>
```

### 3. Stop Ubuntu Only:

```bash
ansible-playbook -i inventory.ini ec2_stop.yaml --vault-password-file vault.pass
```

---

## 💡 Notes

* You must configure AWS credentials using Ansible Vault or environment vars.
* Uses `amazon.aws` collection, so make sure to install it via:

  ```bash
  ansible-galaxy collection install amazon.aws
  ```
* EC2s must have port 22 open for Ansible to connect

---



## 👤 Author

**Deepak** — Final-year AIML student learning DevOps through hands-on AWS automation.

---

## 📜 License

MIT License

---

