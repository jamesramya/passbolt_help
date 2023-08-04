## Prerequisites

For this tutorial, you will need:
- A minimal {{ distributionLabel }} server.
- Passbolt {{ distributionLabel }} package installed.

## Update passbolt
### 1. Take down your site

It is generally a good idea to stop running the site prior to the upgrade. This is to avoid having side effects
such as active users corrupting the data in the middle of an upgrade.

```bash
$ sudo systemctl stop nginx
```

### 2. Backup your database

It is recommended to always perform a backup of your passbolt installation. Please check the [backup](/hosting/backup) article

### 3. Upgrade your system

{% include messages/warning.html
content="**Pro tip:** Sometimes, while updating when there is also an update to MySQL/MariaDB you will get an error on the upgrade step. That's why we are suggesting to manually upgrade passbolt prior to system upgrade"
%}

This commands will trigger an upgrade on your whole {{ distributionLabel }} system:

{% if distributionPackage == 'apt' %}
```bash
sudo {{ distributionPackage }} update
sudo {{ distributionPackage }} --only-upgrade install passbolt-ce-server
sudo {{ distributionPackage }} upgrade
```

{% include messages/notice.html
content="**You are running Passbolt PRO? ↓**"
%}

```bash
sudo {{ distributionPackage }} update
sudo {{ distributionPackage }} --only-upgrade install passbolt-pro-server
sudo {{ distributionPackage }} upgrade
```

{% elsif distributionPackage == 'dnf' or distributionPackage == 'yum' or distributionPackage == 'zypper' %}
```bash
$ sudo {{ distributionPackage }} update
```
{% endif %}
### 4. Clear the cache

Finally make sure you clear the application cache, to make sure any changes in the database structure are
reflected in model cache files:

```bash
$ sudo -H -u {{ webServerUser }} bash -c "/usr/share/php/passbolt/bin/cake cache clear_all"
```

### 5. Bring your site back online

Almost done:
```bash
sudo systemctl start nginx
```