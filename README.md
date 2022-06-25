
### ansible 使用跳板机方式
```
 cat inventory.ini  
[mysql]
192.168.8.114

[prome]
promethues  ansible_ssh_host=192.168.8.211 ansible_ssh_port=22 ansible_ssh_user=root ansible_ssh_private_key_file=/root/.ssh/id_rsa 

[prome:vars]
host_key_checking=False 
ansible_ssh_common_args='-o ProxyCommand="ssh -p 22 admin@192.168.8.114 -W %h:%p"'

[mysql:vars]
host_key_checking=False 
ansible_ssh_common_args='-o ProxyCommand="ssh -p 22 admin@192.168.8.114 -W %h:%p"'
```

