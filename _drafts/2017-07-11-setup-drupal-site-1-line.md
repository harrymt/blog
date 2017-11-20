---
layout: post
title: Install Drupal site with 1 command
---

<div class="message">
Using this 1 line of code, you can setup and install a Drupal 7 website.
</div>


### Line Overview

The following shell script, sets up a Drupal site.

1. Installs composer
2. Downloads Drupal
3. Installs a list of Drupal modules


I also created (another 1 liner for Wordpress](/2017/install-wordpress-with-1-line.md) -- https://gist.github.com/harrymt/6fd60b9eaa2272de64196cad493d7e58. 


#### 1 Line Build

Run this simple command on a server with a LAMP stack in a website directory (e.g. `cd /var/www/MySite.com/public_html`)

The line downloads [this gist](https://gist.github.com/harrymt/89cb1da0b08b8b41efa5b3d3887e34a7) and runs it.

```bash
source <(curl -s https://gist.githubusercontent.com/harrymt/89cb1da0b08b8b41efa5b3d3887e34a7/raw/50eb17909aa186ee60c9bf3ec9d8a0bf07d01116/drupal-7.sh)
```

Or download and manually run the [full script](https://gist.github.com/harrymt/89cb1da0b08b8b41efa5b3d3887e34a7) below.


##### Full Script

```
#!/bin/bash

#
# Install Drupal 7.x on a LAMP stack
#
install_drupal_plugin()
{
	NAME=$1
	php composer.phar require drupal/$NAME
	echo "Installed plugin $NAME"
}

clear
echo "============================================"
echo "Drupal Install Script (takes ~1736s/30m)"
echo "============================================"

if [ $# -ne 4 ]; then
	echo "Project Name:"
	read -e projectname
	echo "Database Name:"
	read -e dbname
	echo "Database User:"
	read -e dbuser
	echo "Database Password:"
	read -s dbpass
else
	projectname=$1
	dbname=$2
	dbuser=$3
	dbpass=$4
fi

echo "============================================"
echo "A robot is now installing Drupal for you."
echo "============================================"

# Track start time
start_time=`date +%s`

# Download + install composer locally
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
rm composer-setup.php

# Create a composer.json file
echo '{ "minimum-stability": "dev", "prefer-stable" : true }' >> composer.json

# Add the ability to require drupal modules
php composer.phar config repositories.drupal composer "https://packages.drupal.org/7"

# # Download drupal framework
# php composer.phar create-project drupal-composer/drupal-project:7.x-dev $projectname --stability dev --no-interaction

# # Setup a project
# cd $projectname/web
# ../vendor/bin/drush site-install --db-url=mysql://$dbuser:$dbpass@localhost/$dbname

# cd ../..

echo "========================="
echo "Installing Drupal 7 Modules."
echo "========================="

# Comment modules you don't want to install
install_drupal_plugin adminimal_admin_menu
install_drupal_plugin admin_views
install_drupal_plugin admin_theme
install_drupal_plugin jquery_update
install_drupal_plugin imagefield_focus
install_drupal_plugin ckeditor_insert
install_drupal_plugin globalredirect
install_drupal_plugin metatag
install_drupal_plugin google_analytics
install_drupal_plugin ctools
install_drupal_plugin entity
install_drupal_plugin entityreference
install_drupal_plugin token
install_drupal_plugin pathauto
install_drupal_plugin ckeditor
install_drupal_plugin weight
install_drupal_plugin fontawesome
install_drupal_plugin site_map
install_drupal_plugin block_class
install_drupal_plugin fontawesome
install_drupal_plugin rules
install_drupal_plugin libraries
install_drupal_plugin webform
install_drupal_plugin image_url_formatter
install_drupal_plugin flexslider
install_drupal_plugin xmlsitemap
install_drupal_plugin less
install_drupal_plugin devel
install_drupal_plugin menu_block
install_drupal_plugin backup_migrate
install_drupal_plugin insert

# Remove bash script if it exists
rm drupal-7.sh

echo "========================="
echo "Installation is complete."
echo Run time is $(expr `date +%s` - $start_time) s
echo "========================="
```
