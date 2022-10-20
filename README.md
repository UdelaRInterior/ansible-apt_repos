Role apt_repos
=========

This role configures the repositories defined in main file `/etc/apt/sources.list`, and eventually those in `/etc/apt/sources.list.d`.

Requirements
------------

This role covers only hosts with apt package management, i.e. Debian distribution or derivatives. 

Role Variables
--------------

To set the host apt repositories, you need to set the flag:
```
apt_repos_management: yes
```
With this very simple set, for Debian and Ubuntu distributions, detecting with ansible facts the distibution, release and version, the role builds the default apt `sources.list` file, and sets the appropriate gpg repositories keys.

Be careful: any previous content in the `/etc/apt/sources.list` will be overwritten.

For Debian and Ubuntu distributions again, you can tune the standard content of this default file with the following versions: 

`apt_repos_url`: the URL of your own or your preferred mirror repository of your distribution,
`apt_repos_security_url`: the URL of your own or your preferred mirror repository for security updates of your distribution (not recommended to be changed)
`apt_repos_components`: the sections or components of your distribution you want to index. A sub-list of `main contrib non-free` for Debian, `main universe multiverse restricted partner` for Ubuntu.
`apt_repos_key_url`: the URL of the GPG key of the repos 


You can also build your own custom `/etc/apt/sources.list` file, overwriting for your host the variable:
```
apt_repositories_sources_list:
- repo: 'deb http://security.debian.org buster/updates main'
  key: 'https://ftp-master.debian.org/keys/archive-key-buster-security.asc'
  comment: Debian security updates
  state: present
- repo: ...
```
`key`, `comment` and `state` are optional, `state` default value is "present".

Finally, you can define extra repositories that will be managed with `apt_repository` ansible module in `/etc/apt/sources.list.d/` folder:
```
apt_repositories_extra:
- repo: deb http://debian.myrepo.org/ buster main
  filename:  my_repo
  state: present
- repo: 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu bionic main'
  filename: ansible_ppa
  keyserver: keyserver.ubuntu.com
  key_id: 93C4A3FD7BB9C367
  state: present
- repo: ...
```

By default, the role only configures and takes off the repos defined in `apt_repositories_extra` list. However, if the role is called with the tag `force-repos` all repositories previously defined in `/etc/apt/sources.list.d/` are wiped.


Example Playbook
----------------

If you run on a debian host:

```
- hosts: servers
  roles:
      - role: UdelaRInterior.apt_repos
        vars:
          apt_repos_management: yes
```

it will replace the  `/etc/apt/sources.list`  with the repositories for the distribution of each server defined in defaults and variables of this role. 

License
-------

GPL-3.0

Author Information
------------------

Daniel Viñar Ulriksen, UdelaR.
