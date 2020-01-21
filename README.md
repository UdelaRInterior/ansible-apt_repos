Role apt_repos
=========

This role configures the repositories defined in main file `/etc/apt/sources.list`, and eventually those in `/etc/apt/sources.list.d`.

Requirements
------------

This role covers only hosts with a Debian distribution or derivative.  

Role Variables
--------------

To use this role, choose first the list of repositories you want to have in `/etc/apt/sources.list`, and define it in your host variables with: 
```
apt_repositories_sources_list:
- repo: 'deb http://security.debian.org buster/updates main'
  key: 'https://ftp-master.debian.org/keys/archive-key-buster-security.asc'
  comment: Debian security updates
  state: present
- repo: ... 
```
`key`, `comment` and `state` are optional, `state` default value is "present".  The `defaults/main.yml` gives an example for the debian. 

Once the repos defined, you can tell the role to manage the repos, setting the variables: 
```
apt_repos_management: yes
```

Be careful: any previous content in the `/etc/apt/sources.list` will be overwritten. 

You can also define extra repositories that will be managed with `apt_repository` ansible module in `/etc/apt/sources.list.d/` folder:  
```
apt_repositories_extra:
- repo: deb http://debian.myrepo.org/ buster main
  filename:  my_repo
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

it will replace the  `/etc/apt/sources.list`  with the repositories defined in default variables 

License
-------

GPL-3.0

Author Information
------------------

Daniel Viñar Ulriksen, UdelaR. 
