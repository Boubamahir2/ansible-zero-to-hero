# How to setup Passwordless Authentication

## virtual machine
## Ansible

### Step 1 — Installing Ansible
To begin using Ansible as a means of managing your server infrastructure, you need to install the Ansible software on the machine that will serve as the Ansible control node.

From your control node, run the following command to include the official project’s PPA (personal package archive) in your system’s list of sources:
```
sudo apt-add-repository ppa:ansible/ansible
```
Press ENTER when prompted to accept the PPA addition.

Next, refresh your system’s package index so that it is aware of the packages available in the newly included PPA:

```
sudo apt update
```

```
sudo apt install ansible
```
Your Ansible control node now has all of the software required to administer your hosts. Next, we will go over how to add your hosts to the control node’s inventory file so that it can control them.

### Step 2 — Setting Up the Inventory File
```
sudo nano /etc/ansible/hosts
```

Note: Although Ansible typically creates a default inventory file at etc/ansible/hosts, you are free to create inventory files in any location that better suits your needs. In this case, you’ll need to provide the path to your custom inventory file with the -i parameter when running Ansible commands and playbooks. Using per-project inventory files is a good practice to minimize the risk of running a playbook on the wrong group of servers.
```
[servers]
server1 ansible_host=203.0.113.111
server2 ansible_host=203.0.113.112
server3 ansible_host=203.0.113.113

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

```
ansible-inventory --list -y
```

### Step 3 — Testing Connection
```
ansible all -m ping -u root
```

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```
```
ssh-add -l
```
```
 cat ~/.ssh/id_rsa.pub | ssh root@server_ip "cat >> ~/.ssh/authorized_keys"
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

