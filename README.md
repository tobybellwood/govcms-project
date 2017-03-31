# govCMS (Drupal 8) BLT

## Installation

### Server Requirements

* Apache, Nginx, Microsoft IIS or any other web server with proper PHP support
* PHP 5.6 or higher
* MySQL 5.5.3/MariaDB 5.5.20/Percona Server 5.5.8 or higher with PDO and an InnoDB-compatible primary storage engine
* PostgreSQL 9.1.2 or higher with PDO
* SQLite 3.7.11 or higher

**Dependencies**

* [Git](http://git-scm.com/)
* [Composer](https://getcomposer.org/)
* [Node](https://nodejs.org/en/), which includes the NPM package manager

## Development with BLT

### Local Development

No matter what local environment you choose to use, the following guidelines should be followed:

* In order to guarantee similar behavior, use Apache as your web server.
* The blt alias must be installed.
* MySQL must use mysql://drupal:drupal@localhost/drupal:3306
* Your LAMP stack must have host entry for http://local.govcms.com/ pointing to docroot
* PHP memory limit >= 2G (required by blt)

1. Enter the project root, and run the following commands in order (Run once):

```
cd MY_PROJECT
composer run-script blt-alias
source ~/.bash_profile
```

2. Update/Create local.alias.drushrc.php in drush/site-aliases

```
<?php

// Local alias.
$aliases['govcms.local'] = array(
    'root' => '/var/www/MY_PROJECT/docroot',
    'uri' => 'http://local.govcms.com',
);
```

3. Build local govCMS instance

Please make sure your host entry and MySQL database meet the above requirements.

```
blt local:setup
```

4. Visit local govCMS instance
```
http://local.govcms.com/
```

5. Sign into govCMS instance as Admin
```
drush @govcms.local uli
```

6. If you'd like to execute Behat tests from the host machine, you will need Java:
```
brew cask install java
brew install chromedriver
```

### Using Drupal VM for local development

1. Download the Drupal VM dependencies listed in [Drupal VM's README](https://github.com/geerlingguy/drupal-vm#quick-start-guide). If you're running [Homebrew](https://brew.sh/index.html) on Mac OSX, this is as simple as:

```
brew tap caskroom/cask
brew install php56 git composer ansible drush
brew cask install virtualbox vagrant
```

2. Enter the project root, and run the following commands in order (Run once):

```
cd MY_PROJECT
composer run-script blt-alias
source ~/.bash_profile
```

3. Customize example.project.local.yml to project.local.yml and run the following to build.

```
blt vm
blt local:setup
```

4. Visit local govCMS instance
```
http://local.govcms.com/
```

5. Sign into  govCMS instance as Admin
```
drush @govcms.local uli
```

6. Drupal VM Dashboard 
```
http://dashboard.local.govcms.com/
```