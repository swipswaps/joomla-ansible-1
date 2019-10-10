
# Joomla site CI CD

1. Create folder `secret` alongside joomla.yml to store your server encrypted details (using ansible vault)

```ini
joomla_user: "username" # Username  to  connect  your  host  through  ssh
joomla_password: "password" # Password  to  connect  your  host  through  ssh
joomla_db: "MYDB" # Database
joomla_host: "localhost" # Database  host
joomla_dbprefix: "z467w_" # Table  prefix
joomla_smtpuser: "" # SMTP  Username
joomla_smtppass: "" # SMTP  Password
joomla_smtphost: "localhost" # SMTP  Host
```

2. Create folder `inventory` alongside joomla.yml to store your server details and Joomla configurations
*E.g* :

*file*: inventory/myserver
```ini
[mysitegroup]
YOUR_SERVER_IP  ansible_host=YOUR_SERVER_HOST  ansible_user={{joomla_user}} ansible_ssh_private_key_file=SSH_KEY_PATH
  
[mysitegroup:vars]
doc_root=/home/{{joomla_user}}/public_html # PATH  to  deploy  Joomla  files
site_id=myserver # Name  of  secret  file
deploy_env_domain=example.com # Site  domain  e.g  example.com
server_runs_as=www-data # Server  user
server_runs_as_group=www-data # Group  of  files
joomla_sitename="core Site" # Overridden  site  name
joomla_log_path="/home/USER_NAME/public_html/logs" # Log  path
joomla_tmp_path="/home/USER_NAME/public_html/tmp" # Tmp  folder  path
```

### Run playbook
```bash
ansible-playbook -i inventory/myserver joomla.yml --vault-password-file=PATH_OF_VAULT_PASSWORD_FILE
```
