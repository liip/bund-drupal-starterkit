Bund-Starterkit for Drupal 8
============================

# What is Bund-Starterkit?
The Bund-Starterkit provides theme and elements based on the official styleguide (version 3.0.0) of the Swiss Federal Administration: http://swiss.github.io/styleguide.
This kit provides a base to quickly implement a website running on Drupal 8 for the Swiss Federal Administration.

Currently, it provides the following elements:

- Multilingual main navigation blocks
- Multilingual service navigation blocks
- Multilingual footer service navigation blocks
- Logo block
- Language switcher block with German, French, Italian, Rumantsch enabled
- Responsive theme for these elements

# Backend requirements
- Drupal 8 requirements in https://www.drupal.org/requirements.
- Drush 8 or later
- Composer (latest)

# Project installation

Download the project (https://github.com/liip/bund-drupal-starterkit/archive/master.zip) and extract it in your work directory. Rename it as you want, let's call it `PROJECT_ROOT` for the rest of this procedure.

Then open a terminal

```
# Install the project with composer
cd PROJECT_ROOT
composer install

```

- Prepare vhost (make sure to point in the `PROJECT_ROOT/web` directory)
- Update your hosts file with the local domain you just set in the vhost
- Now you can run the installation in the browser by selecting the "Bund profile"
  and following the several installation steps or by doing it with drush command
  below:

```
cd PROJECT_ROOT/web
drush site-install bund_drupal_starterkit_profile \
site-default-country=CH date-default-timezone="Europe/Zurich" \
--db-url=mysql://DBUSERNAME:DBPASSWORD@127.0.0.1/db_name \
--account-mail="admin@example.com" \
--account-name=admin \
--account-pass=admin_password \
--site-mail="admin@example.com" \
--site-name="Bund starterkit"
```

# Import contents

It is possible to import dummy contents for menus to have a preview of how
contents are displayed.

```
# Enable migrate_tools and bund_dummy_content modules
drush en -y migrate_tools bund_drupal_starterkit_dummycontent

# Display migration status
drush ms

# Import menu items
drush mi menu_item

# Remove dummy contents
drush mr menu_item
```

To import your own menu items you can use the module bund_drupal_starterkit_dummycontent as an example. It uses a CSV file located in: `modules/custom/bund_drupal_starterkit_dummycontent/data/navigation_menu_item.csv`.

Make sure to respect the structure: `MENU_NAME;ID;Parent_ID;Level_1;Level_2;Level_3`:

- `MENU_NAME` is the menu machine name where the item will be put
- `ID` is a UNIQUE ID for the current menu item
- `Parent_ID` is the ID of the parent menu, leave empty if no parents
- `Level_1-2-3` are the menu level for the menu item. Put here the menu label

Only put one menu item per line in the CSV file.
When the file is complete, run the same command lines as for the dummy content
above.

On the current version, you cannot assign a content to the menu item, you will
have to do it manually in the administration interface.


# Configure languages
By default, all the following languages are enabled:

- German
- French
- Italian
- Rumantch
- English

It is possible to remove languages:

- Connect with the admin user in `/user`
- Go to "Configuration" > "Regional and languages" > "Languages"
- Select the "delete" operation on a language and delete it

If you had some existing blocks shown only on a language you deleted, you will
have to remove them manually in the block interface:

- Go to manage "Structure" > "Block layout" and click the "delete" operation
on the block you would like to delete.


# Frontend

This starterkit use the official styleguide (version 3.0.0) as a submodule. All existing CSS/JS files and assets are imported and available per default, but not necessary integrated as a drupal module at the moment. We highly encourage you to check the official styleguide ( http://swiss.github.io/styleguide/en/index.html ) before adding any new CSS style to your project. Furthermore, we invite you to share any Drupal template matching the styleguide you would develop for your project.

To extend the theme, create a new subtheme based on bund_drupal_starterkit_theme and do not edit the one in theme/contrib, otherwise your changes can be overwritten when doing an update.

# Frontend requirements
- node.js
- npm
- bower

# Frontend development

Install vendors (bootstrap-sass, gulp, gulp-sass, gulp-autoprefixer, browser-sync).
```
npm install
bower install
```

Import css files from submodule and generate js vendors for Drupal
```
gulp init
```

Watch SCSS changes and live reload with browserSync
```
gulp
```

Check the terminal to get the URL from BrowserSync.

