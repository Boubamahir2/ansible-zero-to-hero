# Ansible Configuration File

### 1. Check Current Permissions:
Open a terminal and navigate to the directory where your ansible.cfg file is located.
Use the ls -l command to view the file's permissions:
```
ls -l ansible.cfg
```

### 2. Modify Permissions:
```
chmod 777 ansible.cfg
```
if you want to be the only one to modify this file 
```
chmod 600 ansible.cfg
```

### Running Playbook without Extra Parameters
```
ansible-playbook -i /etc/ansible/hosts -u root --private-key=/path/to/your/private/key first-play.yaml -vvv
```

### Update Inventory File
To make sure that Ansible always uses the root user and the specified private key, you can update your inventory file (/etc/ansible/hosts) as follows:
```
[all]
server1 ansible_host=138.68.80.191 ansible_user=root ansible_ssh_private_key_file=~/.ssh/id_rsa

```

### Update Ansible Configuration File
Alternatively, you can specify the default user and SSH key in your ansible.cfg file. Create or update ansible.cfg in your project directory or in /etc/ansible/:
```
[defaults]
inventory = /etc/ansible/hosts
remote_user = root
private_key_file = ~/.ssh/id_rsa

[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=60s
```

#### To move to the end of the page in Nano, use the following key combination:
### Alt + / (or Ctrl + End)

#### To search for a specfic field:
### Press Ctrl+W 

### Running Playbook without Extra Parameters
After updating the inventory file or configuration file, you can run your playbook without needing to specify the user and private key every time:
```
ansible-playbook first-play.yaml 
```


