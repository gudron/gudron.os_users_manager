gudron.os_users_manager
=========

Role for manage operation system users and groups

Role Variables
--------------

### General variables

  * `users_list_params: list`
    List of users parameters. Like `name`, `shell`, `password` and etc.

    Supported parameters: [defaults/main.yml](defaults/main.yml).

  * `groups_list_params: list`
    List of groups parameters.

    Supported parameters: [defaults/main.yml](defaults/main.yml).


#### Users parameters

  * `name: string`
    User name.

  * `is_sudo: boolean`
    Flag indicating that the user is an sudo.

  * `no_pwd_sudo: boolean`
    Flag indicating that the user can use sudo privelegies without promt password.

  * `password: string`
    User password.

  * `email: string`
    User email.

  * `groups: list`
    The list of groups the user is a member of.

  * `ssh: dict`
    The dictionary of user ssh settings.

    * `keys: list`
      The list of user ssh private and public keys

Dependencies
------------

  * gudron.sudo - [Role for install sudo package and manage sudo privelegies](https://github.com/gudron/gudron.sudo)

Example Playbook
----------------

    - hosts: example_project:&example_project_stage
      any_errors_fatal: "{{ any_errors_fatal | default(true) }}"
      gather_facts: True

      roles:
        - name: gudron.os_users
          vars: 
            groups_list_params:
              - name: example_group

            users_list_params:
              - name: example_user
                is_sudo: true
                no_pwd_sudo: true
                password: "example_password"
                email: example@example.com
                groups:
                  - sudo
                  - example_group
                ssh:
                  keys:
                    - priv: /path/to/existen/ssh/key/ansible_example.pem
                      pub: /path/to/existen/ssh/key/ansible_example.pem.pub
                      comment: ansible_example

License
-------

Apache