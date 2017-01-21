ansible-role-synology-nextcloud
=============

Role to install nextcloud on Synology DSM 6.x.
Inspired and heavily borrowed from
- https://github.com/aalaesar/install_nextcloud

Requirements
------------

Synology DiskStation DSM 6

PHP 7 with the following settings:
- Enable PHP cache
- Customize PHP open_basedir: must include the path to the NC data directory

Tested on
- Synology DS-211+
- Synology DS-415+

Role Variables
--------------
### Installation configuration
> Source location will be calculated following channel, version, branch and archive_type values.

```YAML
nextcloud_channel: "releases"
```
Defines the version channel you want to use for the installation
Available : releases | prereleases | daily | latest
```YAML
nextcloud_version: 10.0.2
```
Specify the version name for channels **releases**, **prereleases** and **daily**. (it may not be numbers at all)
```YAML
nextcloud_branch: "stable"
```
Specify the branch name for **daily** & **latest** channel
```YAML
nextcloud_repository: "https://download.nextcloud.com/server"
```
The Nextcloud's official repository. You may change it if you have the sources somewhere else.
```YAML
nextcloud_archive_type: "tar.bz2"
```
The archive type do download.
Available : zip | tar.bz2

### Main configuration
```YAML
nextcloud_trusted_domain: ["{{ ansible_default_ipv4.address }}"]
```
The list of domains you will use to access the same Nextcloud instance.
```YAML
nextcloud_instance_name: "{{ nextcloud_trusted_domain | first }}"
```
The name of the Nextcloud instance. By default, the first element in the list of trusted domains

```YAML
nextcloud_webroot: "/volume1/web/nc"
```
The Nextcloud root directory.
```YAML
nextcloud_data_dir: "/volume1/webdata/ncdata"
```
The Nextcloud data directory. This directory will contain all the Nextcloud files. Choose wisely.
```YAML
nextcloud_admin_name: "admin"
```
Defines the Nextcloud admin's login.
```YAML
nextcloud_admin_pwd: "secret"
```
Defines the Nextcloud admin's password.

**Not defined by default**

If not defined by the user, a random password will be generated.
### Database configuration
```YAML
nextcloud_db_host: "127.0.0.1"
```
The database server's ip/hostname where Nextcloud's database is located.
```YAML
nextcloud_db_backend: "mysql"
```
Database type used by nextcloud.

Supported values are:
- mysql
- mariadb
- pgsql _(PostgreSQL)_

```YAML
nextcloud_db_name: "nextcloud"
```
The Nextcloud instance's database name.
```YAML
nextcloud_db_admin: "ncadmin"
```
The Nextcloud instance's database user's login
```YAML
nextcloud_db_pwd: "secret"
```
The Nextcloud instance's database user's password.

**Not defined by default.**

If not defined by the user, a random password will be generated.


### System configuration
```YAML
mysql_root_pwd: "secret"
```
root password for the mysql server



## Dependencies



Dependencies
------------

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
