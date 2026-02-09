# Ansible – Simple Explanation with Example

## What is Ansible?

**Ansible** is a simple automation tool used to **configure servers**, **install software**, and **run tasks automatically** on many machines at the same time.

In simple words:

> Instead of logging into 10 or 100 servers and running the same commands again and again, Ansible lets you write the steps once and run them everywhere.

Ansible is:
- Agentless (no software needed on managed servers)
- Uses SSH
- Easy to read (YAML language)
- Widely used for DevOps and cloud automation

---

## Basic Ansible Architecture

- **Control Node**  
  The machine where Ansible is installed (your laptop or a server)

- **Managed Nodes**  
  Servers that Ansible controls (Linux servers, cloud VMs, etc.)

- **Inventory**  
  A file that lists the servers Ansible should manage

- **Playbook**  
  A YAML file that defines what tasks to run

---

## Simple Real-Life Example

### Problem
You want to install **Nginx** on 3 servers.

### Without Ansible
- SSH into server1 → install nginx
- SSH into server2 → install nginx
- SSH into server3 → install nginx

### With Ansible
- Write one playbook
- Run one command
- Nginx installs on all servers

---

## Inventory File Example

**inventory.ini**

```ini
[webservers]
server1 ansible_host=192.168.1.10
server2 ansible_host=192.168.1.11
server3 ansible_host=192.168.1.12
```
## Simple Ansible Playbook Example

`install_nginx.yml`

```yaml
---
- name: Install Nginx on web servers
  hosts: webservers
  become: yes

  tasks:
    - name: Install nginx package
      apt:
        name: nginx
        state: present
        update_cache: yes
```
```
### Run the playbook

```bash
ansible-playbook -i inventory.ini install_nginx.yml
```

---

## Explanation of the Playbook

```yaml
- name: Install Nginx on web servers
```

A human-readable name for the playbook.

```yaml
  hosts: webservers
```

Targets the `webservers` group from the inventory file.

```yaml
  become: yes
```

Runs commands as root (sudo).

```yaml
  tasks:
```

List of tasks to execute.

```yaml
  - name: Install nginx package
```

Description of the task.

```yaml
    apt:
```

Uses the **apt module** (used for Debian/Ubuntu systems).

---

## Most Commonly Used Ansible Parameters (Daily Use)

### 1. `hosts`

Defines which servers the playbook runs on.

```yaml
hosts: webservers
```

---

### 2. `become`

Used to run tasks with sudo/root privileges.

```yaml
become: yes
```

---

### 3. `tasks`

A list of actions Ansible performs.

```yaml
tasks:
  - name: Example task
```

---

### 4. `name`

A readable description for plays and tasks.

```yaml
name: Start nginx service
```

---

### 5. `vars`

Defines variables inside a playbook.

```yaml
vars:
  app_port: 8080
```

Usage:

```yaml
port: "{{ app_port }}"
```

---

### 6. `with_items` / `loop`

Used for looping over a list.

```yaml
loop:
  - nginx
  - git
  - curl
```

---

### 7. `when`

Runs a task only if a condition is true.

```yaml
when: ansible_os_family == "Debian"
```

---

### 8. `register`

Stores the output of a task in a variable.

```yaml
register: nginx_status
```

---

### 9. `debug`

Prints variables or messages.

```yaml
debug:
  var: nginx_status
```

---

### 10. `state`

Defines the desired state of a resource.

```yaml
state: present   # installed
state: absent    # removed
state: started   # service running
state: stopped   # service stopped
```

---

## Commonly Used Modules (Daily Work)

| Module     | Purpose                           |
| ---------- | --------------------------------- |
| `apt`      | Install packages on Ubuntu/Debian |
| `yum`      | Install packages on CentOS/RHEL   |
| `service`  | Start/stop services               |
| `copy`     | Copy files to servers             |
| `template` | Copy files with variables         |
| `file`     | Manage files and directories      |
| `command`  | Run shell commands                |
| `shell`    | Run shell scripts                 |

---

## Why Ansible is Popular

* Easy to learn
* No agents required
* Human-readable YAML
* Scales from 1 server to 1000 servers
* Strong community support

---

## Summary

* Ansible automates repetitive server tasks
* Uses simple YAML files called playbooks
* Saves time and reduces human errors
* Ideal for configuration management and deployments

