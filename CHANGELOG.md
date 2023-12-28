# Changelog of apt_repos ansible role

Migration to [`cielito.system` collection](https://galaxy.ansible.com/cielito/system).

## [v1.3.0](https://github.com/UdelaRInterior/ansible-apt_repos/tree/v1.3.0)

* automation of `apt_repositories_sources_list` (using defaults and vars) for
  Debian and Ubuntu distribution
* introduction of varibales `apt_repos_url`, `apt_repos_security_url`, `apt_repos_components`
  and `apt_repos_key_url` to tune previous automation of sources.list.

## [v1.2.1](https://github.com/UdelaRInterior/ansible-apt_repos/tree/v1.2.1)

* Ensure gpg is installed (not present in debian bullseye, at least proxmox templates)
* Be carefull to your `apt_repositories_sources_list` definition: the `duistrubution field syntax changes for security update. 
  It is  `bullseye-security` and no longer `buster/updates`, `stretch/updates`, ...
* Fixing syntax details


## [v1.2.0](https://github.com/UdelaRInterior/ansible-apt_repos/tree/v1.2.0)

* manages removal of previous config with a variable, because it didn't work with tags

## [v1.1.0](https://github.com/UdelaRInterior/ansible-apt_repos/tree/v1.1.0)

* adds the possibility to add keys with keyserver and id 
* fix bug for source.list keys

## [v1.0.0](https://github.com/UdelaRInterior/ansible-apt_repos/tree/v1.0.0)

* first published version
* establishes the source.list file with a first set of repos
* adds repos to source.list.d form a second set
* adds keys of all repos from URLs
* option to reset all the previously existing repos