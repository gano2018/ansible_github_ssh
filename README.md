Setting to access github by SSH key
===

## Overview

What this role do is two things.

1. Copy your key into $HOME/.ssh/github_key/
2. Insert github access information to $HOME/.ssh/config

## Usage

1. Put the registered ssh keys to files/.
   The key's name should be `id_rsa` for private and `id_rsa.pub` for public.
   Without keys, the roles does not work.

2. Define these variables if you need.

   - `project_name` is a name of the github repository.　The default value is `project`.
     If you define this, you will access the repository by `git@{{ project_name }}:<github_user>/{{ project_name }}.git`

   - `user` is a username who wants to access github. The default value is `{{ ansible_ssh_user }}`
      SSH keys will be copied on `/home/{{ user }}/.ssh/github_keys`.

   - `mark` is a mark for [blockinfile　module](https://docs.ansible.com/ansible/2.5/modules/blockinfile_module.html) of ansilbe.　
     Please read the link for details. The default value is `# SSH_KEY ANSIBLE MANGED BLOCK1`.

## Description

After the role executed, you will see the below in $HOME/.ssh/config

  ```
    Host {{ project_name }}
    Port 22
    HostName github.com
    IdentityFile ~/.ssh/github_keys/{{ project_name }}
    TCPKeepAlive yes
    IdentitiesOnly yes
  ```

so you can access to the github repository by `git@{{ project_name }}:<github_user>/{{ project_name }}.git`  

  　　
