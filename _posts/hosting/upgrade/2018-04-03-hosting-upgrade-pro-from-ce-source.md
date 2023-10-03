---
title: Upgrade Passbolt from CE source install to Pro
card_title: From CE source install
card_teaser: Upgrade from CE source install to Pro
card_position: 7
date: 2018-04-03 00:00:00 Z
description: Upgrade from CE source install to Pro
icon: fa-git
categories: [hosting,upgrade,pro]
sidebar: hosting
layout: default
slug: upgrade-pro-from-ce-source
permalink: /:categories/:slug.html
---

{% include layout/row_start.html %}
{% include layout/col_start.html column="7" %}

This tutorial covers the case where you want to upgrade your current instance of passbolt CE v2.x into Passbolt Pro.

{% include messages/warning.html
    content="**Important:** Please take a full [backup](/hosting/backup) of your Passbolt CE before proceeding with the upgrade. Backup should include passbolt files as well as the database."
%}

{% include messages/notice.html
    content="You may want to consider moving to one of our [packages](/hosting/upgrade) before upgrading to Pro."
%}

## System requirements
{% include hosting/v4-requirements.md %}

## Upgrade to Passbolt Pro
In the following examples we assume you are running passbolt using apache in the `/var/www/passbolt`
directory. You will need to replace these values with your local environment settings.

### 1. Take your site offline & install the required modules
{% include hosting/upgrade/take-your-site-offline.md %}

If you are planning to use LDAP integration you will need to make sure the PHP extension for LDAP
is installed and enabled (for example: `apt-get install php-ldap`). Make sure you restart your webserver
when you add new PHP extensions (for example with: `sudo service restart php-fpm`).

### 2. Download Passbolt Pro
{% include hosting/upgrade/pro/v2/download-and-replace-passbolt.md 
    repo_url="https://bitbucket.org/passbolt_pro/passbolt_pro_api.git"
%}

### 3. Install the dependencies
{% include hosting/install/install-composer-dependencies.md %}

### 4. Copy the avatar folder
```shell
/var/www/passbolt$ cp -R ../passbolt_old/webroot/img/public/* ./webroot/img/public/.
```

### 5. Configure Passbolt Pro
{% include hosting/install/pro/v2/install-with-webinstaller.md %}

### 6. Your server is now ready to run passbolt

Once you have followed all the steps of the wizard, Passbolt Pro is ready to run. You will be redirected
automatically to the login page where you can log in.

### 7. Ensure you don't have duplicate cron jobs

{% include hosting/upgrade/cronjobs.md %}


## That's it!

At this stage, Passbolt Pro should be working perfectly.

Any issue? Do contact us on the [Passbolt Pro support](mailto:contact@passbolt.com) with the email provided during your purchase.

{% include date/updated.html %}

{% include layout/col_end.html %}
{% include layout/col_start.html column="4 last push1" %}

{% include aside/pro-support.html %}

{% include layout/row_end.html %}
