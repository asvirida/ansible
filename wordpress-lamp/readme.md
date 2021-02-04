# Wordpress on Linux

This playbook has been tested on:
- **Ubuntu** 20.04 LTS
- **Debian** 10
- **Centos** 8 (**RedHat**)

## Settings

- `php_modules`: For Debian. An array containing PHP extensions that should be installed to support your WordPress setup. You don't need to change this variable, but you might want to include new extensions to the list if your specific setup requires it.
- `php_modules_redhat`: For RedHat. An array containing PHP extensions that should be installed to support your WordPress setup. You don't need to change this variable, but you might want to include new extensions to the list if your specific setup requires it.
- `mysql_root_password`: The desired password for the **root** MySQL account.
- `mysql_db`: The name of the MySQL database that should be created for WordPress.
- `mysql_user`: The name of the MySQL user that should be created for WordPress.
- `mysql_password`: The password for the new MySQL user.
- `http_host`: Your domain name.
- `http_conf`: The name of the configuration file that will be created within Apache.
- `http_port`: HTTP port for this virtual host, where `80` is the default. 
- `http_old_host`: "OLD_IP_OR_HOST"  for restore backup
- `http_new_host`: "NEW_IP_OR_HOST"  for restore backup
- `mysql_backup_name`: MySQL Backup and Update database. Need set your backup file name in /tmp folder on your pc
- `mysql_j2_name`: MySQL Backup and Update database. Need for update ip or site domain

## Running this Playbook

Quickstart guide for those already familiar with Ansible:

### 1. Obtain the playbook
```shell
git clone https://github.com/asvirida/ansible-playbooks
cd ansible-playbooks/wordpress-lamp
```

### 2. Customize Options

```shell
nano vars/default.yml
```


### 3. Run the Playbook

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

### 4. Restoring the Wordpress database from the backup

4.1 set `mysql_backup_name` in `vars/default.yml`  

4.2 Run playbook_restore_backup_db.yml :  
`ansible-playbook ./wordpress-lamp/playbook_restore_backup_db.yml`

### 5. If you want Update ip or site domain in db  

5.1 Uncomment "Update ip or site domain in db" in `playbook_restore_backup_db.yml`  

5.2 set:  
`http_new_host`  
`http_old_host`  
in `vars/default.yml`  

>where `http_old_host` is the previous site domain, and `http_new_host` is the new site domain. If using an SSL certificate, specify https instead of http 
