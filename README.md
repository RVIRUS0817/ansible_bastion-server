# ansible_bastion-server

![nm_diagram_061316_a1](https://user-images.githubusercontent.com/5633085/49913802-45a79d00-fed2-11e8-9ab6-41f84ed69a0e.png)

## Environment

- Amazon Linux/CentOS  
- localhost   

## Specification
- u have to run localhost  
- User management is done with ansible   
- You can sudo belong to the adachin group   
- Operating so that initial password is managed by ansible but changed 
   - Ansible adds to add a password when new user is created 
- The ssh key should use github 
- If you do not specify a key you are asked for Google Auth's login password and Linux user password (2-step verification) 

## Add user

- user.yml

user Since there is a module to be created and a part to set the public key, add it.

```
  - { name: 'name', pass: "{{ PASS }}", updatepass: 'on_create', shell: '/bin/bash', state: 'present', remove: 'no' }
→add

  - { user: 'name', key: 'sshxxxxxxxxxxxxxxxxxxxxxxx' }
→add
```

## Apply

```
$ git pull
$ ansible-playbook -i hosts pre.yml -KDC
$ ansible-playbook -i hosts pre.yml -KD
$ sudo passwd -e username
```

## Delete user

- user.yml

```
 - { name: 'name', pass: "{{ PASS }}", groups: 'adachin', shell: '/bin/bash', state: 'absent', remove: 'yes' }
```

- Apply

```
$ git pull
$ ansible-playbook -i hosts pre.yml -KDC
$ ansible-playbook -i hosts pre.yml -KD
$ sudo passwd -e username
```

- Delete code user


```
 - { name: 'name', pass: "{{ PASS }}", groups: 'adachin', shell: '/bin/bash', state: 'absent', remove: 'yes' }
→delete

  - { user: 'name', key: 'sshxxxxxxxxxxxxxxxxxxxxxxxxxx' }
→delete
```

