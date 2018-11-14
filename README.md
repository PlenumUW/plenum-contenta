<h1 align="center"><img src="http://students.washington.edu/plenum/images/logo2-300x300-white.png"/></h1>

Plenum is an online journal devoted to showcasing the highest quality scholarship in undergraduate geography while building community amongst the Geography Department at the University of Washington. It is managed, produced, and reviewed by undergraduate students from the Department of Geography at the UW.

# Plenum Website Back-End
Plenum's back-end is a custom [Contenta CMS](https://www.contentacms.org), an open-source and API-first distribution of Drupal 8. This back-end is used to manage Plenum content and expose the content via a JSON API, which is then accessed via the front-end website.

![alt text](https://lh3.googleusercontent.com/Unh778hIS1-eYOlWDLcGFTfuw2rm1fyYxt7PEB1eDa9V1prqwqzvNd62CDJbyq8Kh-WjqHcVwTDFxt0Ko8IiQSqYajHDYaML8fo=w8128-h4976-rw-no "Plenum content management system GUI example")

# Local Install
## Requirements
* Github Account - Sign up for the [student developer pack](https://education.github.com/pack) for freebies
* Access to Plenum's Dev Team Google Drive - Contact plenum@uw.edu with your uw email to get access
* A LAMPy software stack - [MAMP](https://www.mamp.info/en/) is a great solution
* [Composer](https://getcomposer.org/download/) 

## Getting Setup
1. [Clone](https://help.github.com/articles/cloning-a-repository/) this repo into the hosted directory of your LAMPy stack (/MAMP/htdocs/)
2. Install project dependencies with Composer, this will take a few minutes... During installation, go to step 3
```
cd /plenum-contenta
composer install
```
3. Within MySQL create a new database--name it 'contenta' and choose the 'utf8mb4_unicode_ci' collation.
4. Create a file titled '.env' at the root directory of the project and input the following and replace {{variables}} with relevant information. If you're using MAMP, this info can be found at the 'WebStart' page.
```
# Example .env file.
SITE_MAIL=admin@localhost
ACCOUNT_MAIL=admin@localhost
SITE_NAME='Plenum Contenta - Local'
ACCOUNT_NAME=admin
MYSQL_DATABASE=contenta
MYSQL_HOSTNAME=localhost
MYSQL_PORT={{MYSQL_PORT}}
MYSQL_USER={{MYSQL_USER}}}}
```
5. Create a file titled '.env.local' at the root directory of the project and input the following and replace {{variables}} with relevant information. If you're using MAMP, this info can be found at the 'WebStart' page.
```
# Example .env file.
MYSQL_PASSWORD='{{MYSQL_PASSWORD}}'
ACCOUNT_PASS=admin
```
6. Run `composer install:with-mysql` and wait a few minutes to finish installing
7. Once install is finished, change the site UUID
```
drush config-set "system.site" uuid dc6a60d1-2b77-4068-aebb-03aaca963536
```
8. Uninstall included content.
   1. In browser, navigate to the CMS. Something like 'http://localhost:8888/plenum-contenta/web'
   1. Sign in with U:'admin' P:'admin', or whatever you put in the '.env' files for ACCOUNT_... variables
   2. Go to _Advanced -> Extend -> Uninstall_
   3. Uninstall 'Recipes Magazin'. This is a sample content module that comes with Contenta CMS.
9. Import Plenum content
   1. Download [_Plenum Backup GZIP_](https://drive.google.com/open?id=1jwrCoFplMZct4cwFns3X-arbX44uEF84)
   1. In the CMS, navigate to _Configuration -> Development -> Backup & Migrate_
   2. Import the downloaded backup
      - Sign back in if you get signed out following a successful import
   3. Download the [public files](https://drive.google.com/open?id=12NRFl9aVZPghO-AVGN2w9wTGvL9VIjaU)
   4. Unzip the _public files_ in the local directory _../plenum-contenta/web/sites/default/files/_

Congratz! You are ready to develop!
