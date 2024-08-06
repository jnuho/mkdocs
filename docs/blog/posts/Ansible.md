---
draft: false
date: 2024-06-01
categories:
  - Ansible
authors:
  - junho
---

Ansible playbook

<!-- more -->

# Table of contents

- [Ansible](#ansible)


## Ansible

We can automate some aspects of the Cloud Native application lifecycle using Ansible.

```sh
# install python
sudo apt install python3 python3-venv python3-pip -y
python3 -V

echo -e "import sys\nprint(sys.version)" > python3_test.py
python3 python3_test.py
  3.12.3 (main, Apr 10 2024, 05:33:47) [GCC 13.2.0]
rm python3_test.py


cd ~
python3 -m venv .venv
source .venv/bin/activate

pip install ansible
ansible --version
pip install --upgrade ansible
```

- inventory

```
# Before writing the playbook, create a file named inventory to tell Ansible how to connect to localhost:
[localhost]
127.0.0.1   ansible_connection=local
```

- playbook

```yml
# main.yml
---
- hosts: localhost
```

Now Run the ansible playbook!

```sh
ansible-playbook -i inventory main.yml
```

The best Ansible playbooks are idempotent, meaning you can run them more than one time,
and assuming the system hasn’t been changed outside of Ansible,
you’ll see no changes reported after the first time the playbook is run.
This is helpful for ensuring a consistent state across your application deployments,
and to verify there are no changes (intended or not) happening outside of your automation.


- install go

```
wget https://go.dev/dl/go1.22.5.linux-arm64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.22.5.linux-arm64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc
source ~/.zshrc
```

[↑ Back to top](#)
<br><br>



