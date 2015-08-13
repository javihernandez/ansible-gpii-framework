# GPII Framework Ansible Role

This role automates the provisioning of the [GPII Framework](https://github.com/gpii/linux) on Fedora. It relies heavily on a [Node.js role](https://github.com/avtar/ansible-nodejs) to do most of its work.

The GPII Framework tests require that the ``~/.local/share/orca`` directory exists. Currently this role ensures that Orca is started at least once so that the Orca directory is created before any tests are run.

## Role Variables

Please refer to the [defaults/main.yml](https://github.com/avtar/ansible-gpii-framework/blob/master/defaults/main.yml) file for a list of variables.

## Requirements

The following roles are required:

*  [facts](https://github.com/avtar/ansible-facts/)
*  [nodejs](https://github.com/avtar/ansible-nodejs/)

## Example

Here is an example playbook that uses this role:

```
- hosts: localhost
  user: root

  vars:
    nodejs_app_name: gpii-linux-framework
    nodejs_app_git_repo: https://github.com/gpii/linux.git
    nodejs_app_git_branch: master
    nodejs_app_rpm_packages:
      - nodejs-grunt-cli
      - orca
      - glib2-devel
      - PackageKit-glib-devel
      - json-glib-devel
      - libXrandr-devel
      - libXrender-devel
      - libX11-devel
      - xorg-x11-proto-devel
      - alsa-lib-devel
      - tuxguitar
    nodejs_app_commands:
      - npm install
      - grunt --force build
    nodejs_app_start_script: gpii.js
    nodejs_app_install_dir: /home/vagrant/gpii-framework
    nodejs_app_git_clone: false

  roles:
    - facts
    - nodejs
    - gpii-framework
```
