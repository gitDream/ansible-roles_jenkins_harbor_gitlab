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
