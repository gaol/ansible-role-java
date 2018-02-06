# ansible-role-package

This Ansible role has very simple goal to just install defined packages

In most common cases, only one variable needs to be defined:

    desired_packages:
      - java-1.8.0-openjdk-devel
      - maven
      - docker

Then this role will just install the packages defined above.

In RPM based package manager, `some-yum.repo` may need to be installed first, and also some rpm keys, then the following variables can be defined:

        yum_repo_urls:
          - https://pkg.jenkins.io/redhat/jenkins.repo
    
        yum_repo_key_urls:
          - https://pkg.jenkins.io/redhat/jenkins.io.key

In Fedora and CentOS, `epel-release` is a special package which needs to be installed before some other packages can be installed, such packages can be defined in:

        pre_packages:
          - epel-release

In many cases, some services need to be started after package installation, just define them in:

        started_services:
          - docker

### Full Examples:

    ---
    - hosts: all
      become: yes
      become_user: root
      vars:
        yum_repo_urls:
          - https://pkg.jenkins.io/redhat/jenkins.repo
    
        yum_repo_key_urls:
          - https://pkg.jenkins.io/redhat/jenkins.io.key
    
        pre_packages:
          - epel-release
    
        pre_services: []
    
        scripts_after_pre_services:
          - dummy_1.sh
    
        desired_packages:
          - java-1.8.0-openjdk-devel
          - maven
          - docker
    
        configs_after_install:
          - src: "{{ playbook_dir }}/local"
            dest: "/tmp/gaol.package.test"
    
        started_services:
          - docker
    
        scripts_after_services_started:
          - dummy_2.sh
    
      roles:
        - gaol.package

