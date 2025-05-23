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
    clustershell_packages:
      - clustershell

    # List of example group bindings to enable
    # e.g. to install Slurm group bindings:
    # clustershell_group_bindings:
    #   - slurm
    #
    # This will copy slurm.conf.example to slurm.conf
    clustershell_group_bindings: []

    # List of custom group bindings
    # clustershell_group_bindings_custom:
    #   - name: racksdb
    #     content: |
    #       [racksdb]
    #       map:     racksdb nodes --infrastructure atlas --tags $GROUP --list
    #       all:     racksdb nodes --infrastructure atlas --list
    #       list:    racksdb tags  --infrastructure atlas --on-nodes
    #       reverse: racksdb tags  --node $NODE
    #
    # This will install file racksdb.conf
    clustershell_group_bindings_custom: []

    # List of group bindings to remove
    clustershell_group_bindings_remove: []

    # Configuration for sshpass mode (added in ClusterShell 1.9)
    # Set 'clustershell_sshpass: true' to enable sshpass mode
    clustershell_sshpass: false
    clustershell_sshpass_password_prompt: 'yes'
    clustershell_sshpass_ssh_path: /usr/bin/sshpass /usr/bin/ssh
    clustershell_sshpass_scp_path: /usr/bin/sshpass /usr/bin/scp
    clustershell_sshpass_ssh_options: -oBatchMode=no -oStrictHostKeyChecking=no

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
