# Setup EC2 Collection and Authentication

## Install boto3

```
pip install boto3
```

## Install AWS Collection

```
ansible-galaxy collection install amazon.aws
```

## Setup Vault 

1. Create a password for vault

```
openssl rand -base64 2048 > vault.pass
```

2. Add your AWS credentials using the below vault command

```
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```

3. edite vault password

```
ansible-vault edite group_vars/all/pass.yml --vault-password-file vault.pass
```
4. execute ansible playbook with vault password

```
ansible-playbook <playbook> --vault-password-file vault.pass
```
or
```
ansible-playbook -i inventory.ini your_inventory.yaml --vault-password-file vault.pass
```





