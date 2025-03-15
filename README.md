ClusterShell
============

This role installs the [ClusterShell][1] software and defines groups of nodes
based on the groups declared in the Ansible inventory.

[1]: https://cea-hpc.github.io/clustershell/

Requirements
------------

The below Python requirements are needed on the host that executes this role.

 - clustershell

Role Variables
--------------

    ---
    # List of packages to install
    clustershell_packages: clustershell

    # Configuration for sudo mode (added in ClusterShell 1.9)
    # Set 'clustershell_sudo: true' to enable sudo mode
    clustershell_sudo: false
    clustershell_sudo_password_prompt: 'yes'
    clustershell_sudo_command_prefix: /usr/bin/sudo -S -p "''"

Example Playbook
----------------

Install and configure clustershell:

    - hosts: headnodes
      roles:
        - role: btravouillon.clustershell
          tags: 'role::clustershell'

Install ClusterShell with Python 3 support:

    - hosts: headnodes
      roles:
        - role: btravouillon.clustershell
          clustershell_packages: ['clustershell', 'python36-clustershell']

Instructions
------------

To check the groups, run the command below:

    $ nodeset -LL
