# Ansible Realtime project

## Task 1

Create three(3) EC2 instances on AWS using Ansible loops
- 2 Instances with Ubuntu Distribution
- 1 Instance with Centos Distribution

Hint: Use `connection: local` on Ansible Control node.

## Task 2

Set up passwordless authentication between Ansible control node and newly created 
instances.

## Task 3

Automate the shutdown of Ubuntu Instances only using Ansible Conditionals

Hint: Use `when` condition on ansible `gather_facts`

## Debug Ansible using facts
```---
- hosts: all
  become: true
  tasks:
  - name: Print all available facts
    ansible.builtin.debug:
      var: ansible_facts 
```


To see the ‘raw’ information as gathered, run this command at the command line:

``` ansible <hostname> -m ansible.builtin.setup ```

## Debug Ansible using gatherfacts
```---
- hosts: all
  become: true
  tasks:
  - name: Print all ansible gathhered ansible_facts
    ansible.builtin.debug:
      var: ansible_facts 
```
