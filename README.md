# .vhosts
Lightweight VirtualHost manager for Mac. A MAMP alternative.

**Changes to this fork:**
- Fixed Apache commands (restart, start, and stop)
- Added support for custom messages
- Disabled restart-apache-button for now

**Roadmap for this fork:**
- Proper support for sub-directories

## Features
- Add and modify localhost VirtualHosts
- Autoload `.vhosts` files from project folders and insert them into global `httpd-vhosts.conf`

![Alt text][screenshot]

## Install
1. Clone repository to ~/Sites

2. `sh boostrap.sh`

**Requirements:**

1. Apache 2 (Built into Mac OS X)

**Optional:**

1. [Hosts.prefpane](https://github.com/specialunderwear/Hosts.prefpane/downloads)
2. MySQL [dev.mysql.com](https://dev.mysql.com/downloads/mysql/) - [Useful settings](http://www.sequelpro.com/docs/Where_are_MySQLs_Files)
3. nginx `brew install nginx`
4. redis [redis.io](http://redis.io/download)


##.vhosts File
You can add a .vhosts file into the root of your project directory and it will automatically be loaded into your VirtualHosts the next time you visit `http://vhosts.localhost`. Project folders in `~/Sites` are scanned by default, you can add a custom one by adding to the `dirs` array in `json/config.json`. `__DIR__` will automatically be replaced with the project directory.

### users/username.conf
```bash
# Defaults applied to all directories listed in json/config.json['dirs']
<Directory "/Users/username/.vhosts">
    Options Indexes MultiViews Includes ExecCGI
    AllowOverride All
    Order Deny,Allow
    Allow from all
</Directory>
```

### Sample .vhosts File
```bash
# VirtualHosts for Yeoman projects
<VirtualHost *>
    ServerName yeoman
    DocumentRoot __DIR__
</VirtualHost>

<VirtualHost *>
    ServerName app.yeoman
    DocumentRoot __DIR__/app
</VirtualHost>

<VirtualHost *>
    ServerName dist.yeoman
    DocumentRoot __DIR__/dist
</VirtualHost>

<VirtualHost *>
    ServerName test.yeoman
    DocumentRoot __DIR__
    <Directory>
        DirectoryIndex test/e2e/runner.html
    </Directory>
</VirtualHost>
```

### Flow of Information
![Alt text][process]

## Terminal
### Apache
```bash
sudo apachectl -k start
sudo apachectl -k restart
sudo apachectl -k stop
```

### nginx
```bash
sudo nginx
sudo nginx -s stop
```

### MySQL
```bash
sudo /usr/local/mysql/support-files/mysql.server start
sudo /usr/local/mysql/support-files/mysql.server stop
```
## Roadmap
- port support
- nginx support
- debug on clean machine of clean install
- yum package to monitor for new .vhosts files

[process]: ./screenshots/process.png "Flow of VirtualHost settings"
[screenshot]: ./screenshots/screenshot.png "Screenshot of .vhosts Dashboard"
