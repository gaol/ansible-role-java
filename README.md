# ansible-role-package

This Ansible role has very simple goal to just install defined packages

In most common cases, only one variable needs to be defined:

    to_be_installed_packages:
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

        prerequisite_packages:
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
    
        prerequisite_packages:
          - epel-release
    
        prerequisite_services: []
    
        prerequisite_scripts:
          - dummy_1.sh
    
        to_be_installed_packages:
          - java-1.8.0-openjdk-devel
          - maven
          - docker
    
        started_services:
          - docker
    
        run_scripts:
          - dummy_2.sh
    
      roles:
        - gaol.package


