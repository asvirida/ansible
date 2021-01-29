# Wordpress on Ubuntu 20.04 LAMP

This playbook will install a WordPress website on top of a LAMP environment (**L**inux, **A**pache, **M**ySQL and **P**HP) on an Ubuntu 18.04 machine, as explained in the guide on [How to Use Ansible to Set Up Wordpress on Ubuntu 18.04 LAMP](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04). A virtualhost will be created with the options specified in the `vars/default.yml` variable file.

## Settings

- `php_modules`:  An array containing PHP extensions that should be installed to support your WordPress setup. You don't need to change this variable, but you might want to include new extensions to the list if your specific setup requires it.
- `mysql_root_password`: The desired password for the **root** MySQL account.
- `mysql_db`: The name of the MySQL database that should be created for WordPress.
- `mysql_user`: The name of the MySQL user that should be created for WordPress.
- `mysql_password`: The password for the new MySQL user.
- `http_host`: Your domain name.
- `http_conf`: The name of the configuration file that will be created within Apache.
- `http_port`: HTTP port for this virtual host, where `80` is the default. 

## Running this Playbook

Quickstart guide for those already familiar with Ansible:

### 1. Obtain the playbook
```shell
git clone https://github.com/asvirida/ansible-playbooks
cd ansible-playbooks/wordpress-lamp_ubuntu20
```

### 2. Customize Options

```shell
nano vars/default.yml
```

```yml
---
#System Settings
php_modules: [ 'php-curl', 'php-gd', 'php-mbstring', 'php-xml', 'php-xmlrpc', 'php-soap', 'php-intl', 'php-zip' ]

#MySQL Settings
mysql_root_password: "mysql_root_password"
mysql_db: "wordpress"
mysql_user: "sammy"
mysql_password: "password"

#HTTP Settings
http_host: "your_domain"
http_conf: "your_domain.conf"
http_port: "80"
```

### 3. Run the Playbook

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

For more information on how to run this Ansible setup, please check this guide: [How to Use Ansible to Install and Set Up WordPress with LAMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04).


### 4. Restoring the Wordpress database from the backup

4.1 set `mysql_backup_name` in `vars/default.yml`  

4.2 Run playbook_restore_backup_db.yml :  
`ansible-playbook ./wordpress-lamp_ubuntu20/playbook_restore_backup_db.yml`

### 5. If you want Update ip or site domain in db  

5.1 Uncomment "Update ip or site domain in db" in `playbook_restore_backup_db.yml`  

5.2 set:  
`http_new_host`  
`http_old_host`  
in `vars/default.yml`  

>where `http_old_host` is the previous site domain, and `http_new_host` is the new site domain. If using an SSL certificate, specify https instead of http 
