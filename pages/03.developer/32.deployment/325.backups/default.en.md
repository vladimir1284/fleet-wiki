# Backup to Google Drive

# Installing Rclone

We use [rclone](https://rclone.org/install/) for baking up relevant server data to google drive.

We the configure the google drive as explained [here](https://rclone.org/drive/).

The following configuration is used:

```
client_id = [TAKEN FROM credentials.json]
client_secret = [TAKEN FROM credentials.json]
service_account_file = gestor/trailer-rental-323614-d43be7453c41.json
```