---
layout: post
title: "Deploying Phoenix 1.4 Application with Ansible and Vagrant"
categories: phoenix elixir deployment ansible vagrant
---

Alternative:
- Setting up build server
- Setting up production server
- Using mix release
- Configure Pheonix app
- Build script
- Deploy script

Orignal:
- Tools involved:
    - Ansible
    - Distillery to build release
    - Vagrant to setup build server and test locally
- Setting Up Vagrant Build and Prod Server
    - Vagrantfile to configure server to be setup
- Ansible script to setup build server
    - Install Node.js
    - Install Erlang
    - Install Elixir
    - Setup ssh key to pull private repository
- Ansible script to setup prod server
    - firewall
    - security
    - nginx
- Ansible script for first build on build server
- Ansible script for first deploy to prod server
- Ansible script for upgrade build on build server
- Ansible script for upgrade deploy on prod server
    - Upgrade mix.exs version
    - Upgrade app version on main.yml
    - Run ansible-playbook

- Limitations
    - Security of the playbook
        - We didn't use the vault feature
        - So, it is not recommended to push the playbook online
    - Currently it use hot upgrade deployment
    - There is a lot of caveats with using hot upgrade
        - Database migration
        - Data Structure migration
    - Quick restart might be better.

- Futures
    - One off script to deploy initial release.
    - One off script to deploy upgrade.
    - Remove the need to upgrade app version on variable files

- References:
    - Distillery Documentations
    - Ansible Phoenix Deployment Blog
    - Ansible for DevOps






