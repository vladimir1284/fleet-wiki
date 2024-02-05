# Backup to Google Drive

## Installing Rclone

We use [rclone](https://rclone.org/install/) for baking up relevant server data to google drive.

We the configure the google drive as explained [here](https://rclone.org/drive/).

The following configuration is used:

```
client_id = [TAKEN FROM credentials.json]
client_secret = [TAKEN FROM credentials.json]
service_account_file = gestor/trailer-rental-323614-d43be7453c41.json
```

## Backup odoo

```bash
#!/bin/bash

# vars
BACKUP_DIR=/home/vladimir/odoo_backups
ODOO_DATABASE=[DATABASE]
ADMIN_PASSWORD=[PASSWORD]

# create a backup directory
mkdir -p ${BACKUP_DIR}

# create a backup
curl -X POST \
    -F "master_pwd=${ADMIN_PASSWORD}" \
    -F "name=${ODOO_DATABASE}" \
    -F "backup_format=zip" \
    -o ${BACKUP_DIR}/${ODOO_DATABASE}.$(date +%F).zip \
    https://odoo.ladetec.com/web/database/backup

# backup to drive
sleep 1
rclone sync ${BACKUP_DIR} remote:odoo

# delete archives older than 7 days from disk
sleep 1
find ${BACKUP_DIR}/ -type f -name "*.tar.gz" -mtime +7 -exec rm {} \;
```
We create the remote directory for storing backups `rclone mkdir remote:odoo`. Then, we add the following configuration line to the **crontab**.

```conf
#/etc/crontab
# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
23 5	* * *   root    /home/vladimir/odoo_backup.sh
```

Finally check that file is uploaded correctly by running:

```bash
sudo ./run-as-cron /home/vladimir/odoo_backup.sh
rclone ls remote:odoo
```

The *run as cron* script test our backup script under the cron environment.


```bash
#run-as-cron
#!/bin/bash
/usr/bin/env -i $(cat /home/username/tmp/cron-env) "$@"
```