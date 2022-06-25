
### ansible 使用跳板机方式
```
[root@jenkins ansible]# cat inventory.ini  

[nginx]
promethues  ansible_ssh_host=192.168.8.211 ansible_ssh_port=22 ansible_ssh_user=root ansible_ssh_private_key_file=/root/.ssh/id_rsa 

[nginx:vars]
host_key_checking=False 
ansible_ssh_common_args='-o ProxyCommand="ssh -p 22 admin@192.168.8.114 -W %h:%p"'

```
### playbook结构
```
[root@jenkins ansible]# tree .
.
├── nginx.yaml
└── roles
    ├── README.md     # 说明文件
    ├── defaults
    │   └── main.yml  # 可被覆写的变数。
    ├── files         # 需复制到 Managed node 的档案。
    │   └── nginx-1.21.6.tar.gz    
    ├── handlers 
    │   └── main.yml  # 主要的 handler。
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml  # 主要的 task。
    ├── templates     # 集中存放 Jinja2 模板的目录。
    │   └── nginx.conf.j2
    └── vars
        └── main.yml  # 不该被覆写的变数。
 ```       
 ### ansible传入变量方式
 ```
 ansible-playbook -i inventory.ini playbooks/nginx.yml -v -e 'hosts=nginx' 
 ansible-playbook -i inventory.ini playbooks/nginx.yml -v -e '@vars.yaml' 
  
 ```
