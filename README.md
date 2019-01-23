Ansible Role: EPEL Repository
EPEL使用*阿里源 EPEL docker官方* 作为yum源，并工作在CentOS_7.X操作系统上。

要求
此角色仅在CentOS及其衍生产品上运行。

测试环境
ansible 2.7.5-1.el7 os Centos 7.3 X64

角色变量
角色默认变量都放在 RolesName/defaults/main.yml文件中:

流程：
  1 add mirrors.aliyun.com  repo
  2 add epel-release docker.repo
  3 install wget git net-tools ntpdate yum-utiles
  4 install docker-ce-1.8.x   docker-compose
  5 roles:
      docker-compose-jenkins.yml
      docker-compose-gitlab.yml
      docker-compose-harbor.yml

github地址
https://github.com/gitDream/ansible-role-jenkins_gitlab_harbor.git

Example Playbook

- hosts: all
  remote_user: root
  roles:
  - epel
  - docker

- hosts: node_50
  remote_user: root
  roles:
  - dockerJenkins
  - {role: dockerGitlab, docker_Gitlab_path: "/docker-compose/docker-gitlab.yml" }

- hosts: node_60
  remote_user: root
  roles:
  - dockerGitlab
  - {role: dockerGitlab, docker_Gitlab_path: "/docker-compose/docker-gitlab.yml" }

- hosts: node_70
  remote_user: root
  roles:
  - dockerHarbor
  - {role: dockerGitlab, docker_Gitlab_path: "/docker-compose/docker-gitlab.yml" }


未完 测试阶段。。。。。。。。。。！
{files,templates,vars,handlers,meta,default,tasks} 

tasks : 用于存放role_A的主要任务，也可以添加其他task文件，供main.yaml调用，从而实现更加复杂的部署功能。
handlers : 用于存放触发执行（ hanlders ）的任务。
defaults : 用于存放默认变量，优先级最低，变量优先级可参考《ansible基础-变量》。
vars : 用于存放变量文件，role_A中任务和模版里用到的变量可以在这里定义。
files ：用于存放需要拷贝到目的主机的文件，例如，作为「copy」模块src参数的默认根目录。
template : 用于存放模版文件，格式为.j2，文件内容要符合Jinja2语法规则，通常使用「template」模块部署服务的配置文件。
meta : 用于存放role依赖列表，这个知识点后面会详细阐述。
tests : 用于存放测试role本身功能的playbook和主机定义文件，在开发测试阶段比较常用。

在各roles目录下创建 vars/main.yml 重写变量 默认变量目录 default/main.yml
