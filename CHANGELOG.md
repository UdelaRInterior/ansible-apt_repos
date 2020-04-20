# Changelog of apt_repos ansible role

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