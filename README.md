# Upgrade Java - Ansible Automation

## Overview
This repository contains an Ansible-based automation playbook and roles for upgrading Java on Linux servers. The playbook downloads the Java package from Artifactory, extracts it, and configures it appropriately.

## Features
- Downloads Java from Artifactory dynamically based on a variable.
- Renames the existing Java directory for backup.
- Creates a new Java directory if not already present.
- Extracts the downloaded Java package.
- Preserves and restores `cacerts` to retain existing trusted certificates.
- Cleans up old Java installations after a successful upgrade.
- Supports customization through variables.

## Repository Structure
```
upgrade-java/
├── upgradejava.yml          # Main Ansible playbook
├── roles/
│   ├── upgrade_java/
│   │   ├── tasks/
│   │   │   ├── main.yml
│   │   │   ├── rename_java.yml
│   │   │   ├── directory.yml
│   │   │   ├── java.yml
│   │   │   ├── systemd_unit.yml
│   │   │   ├── deletejava.yml
│   │   ├── vars/
│   │   │   ├── main.yml
```

## Installation
1. Install Ansible on your control machine:
   ```sh
   sudo apt update && sudo apt install ansible -y  # Ubuntu/Debian
   sudo yum install ansible -y  # RHEL/CentOS
   ```
2. Clone the repository:
   ```sh
   git clone https://github.com/your-repo/upgrade-java.git
   cd upgrade-java
   ```
3. Update the `vars/main.yml` file with appropriate values:
   ```yaml
   Appcode: "your_app_code"
   user: "your_username"
   group: "your_group"
   Description: "Java Upgrade"
   servicefile: "your_service_file"
   jdkdirectory: "jdk-17"
   java_package: "jdk-17.0.13_linux-x64_bin.tar.gz"
   ```

## Usage
Run the playbook using Ansible:
```sh
ansible-playbook -i inventory upgradejava.yml
```
- Replace `inventory` with your Ansible inventory file containing target hosts.

## Variables
| Variable      | Description |
|--------------|-------------|
| `Appcode` | Application-specific identifier |
| `user` | User that owns the Java installation |
| `group` | Group that owns the Java installation |
| `Description` | Description of the Java upgrade |
| `servicefile` | Name of the service file for Java applications |
| `jdkdirectory` | Directory name of the Java installation |
| `java_package` | Name of the Java package to download from Artifactory |

## License
This project is licensed under the MIT License.


## Troubleshooting
- Ensure the Artifactory URL and package name are correctly set in `vars/main.yml`.
- Verify that Ansible has SSH access to the target servers.
- Check logs using `-vvv` for debugging:
  ```sh
  ansible-playbook -i inventory upgradejava.yml -vvv
  ```

---

Enjoy automated Java upgrades! 🚀

