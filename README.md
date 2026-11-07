# AnsibleForms Automation Repository

This repository hosts the Infrastructure-as-Code (IaC) configuration for **AnsibleForms**. It cleanly separates the user-facing web user interface (UI) components from the backend Ansible automation logic.

---

## 📁 Repository Directory Structure

```text
├── config.yaml          # Global application & UI customization settings
├── forms/               # Web UI Form definitions (YAML)
│   ├── personal_info_form.yml
│   └── server_provision_form.yml
├── playbooks/           # Core Ansible Playbooks executed by forms
│   ├── user_info.yml
│   └── provision.yml
├── vars/                # Global default/environment variable files
│   ├── dev_vars.yml
│   └── prod_vars.yml
└── roles/               # Reusable Ansible roles for modular automation
    └── common_setup/
        ├── tasks/
        │   └── main.yml
        └── defaults/
            └── main.yml
```

---

## 🔍 Directory Breakdown & Core Functions

### ⚙️ `config.yaml`
The global configuration file for your AnsibleForms instance. It controls overall application behavior, user authentication integrations, global environment variables, and theme customizations.

### 📝 `forms/`
Contains the **YAML form definitions** that generate the user-facing web interface.
* Each file represents an interactive form presented on the platform dashboard.
* Form schemas map text boxes, dropdowns, and checkboxes to runtime variables.
* **Key Parameter:** Inside each form YAML, the `playbook:` parameter links the form directly to its corresponding file in the `playbooks/` directory.

### 🚀 `playbooks/`
Houses the primary **Ansible Playbooks** triggered by form submissions.
* Playbooks in this directory do not contain hardcoded user data.
* They dynamically ingest the variables passed securely from the `forms/` web interface at runtime.

### 📦 `roles/`
Follows standard Ansible development practices by housing **modular, reusable automation components**.
* Complex logic, templates, and multi-stage tasks should be broken down into roles.
* Keeping heavy execution logic inside roles ensures that master playbooks remain short, clean, and highly scannable.
* **`roles/<role_name>/defaults/main.yml`**: The ideal location for baseline fallback variables.

### 📊 `vars/`
An optional directory used for managing static environment configuration matrices (e.g., mapping target subnets or API endpoints distinct to `dev` vs. `prod` environments).

---

## 🔄 Deployment & Git Workflow

1. **Development:** Always create a feature branch (`feature/your-change`) to add or modify forms and playbooks.
2. **Testing:** Point a staging instance of AnsibleForms to your feature branch to preview UI adjustments and test playbook execution safely.
3. **Production:** Merge verified code changes into the `main` branch. The production AnsibleForms instance will sync via webhook or routine polling interval, instantly making form updates live for end-users.