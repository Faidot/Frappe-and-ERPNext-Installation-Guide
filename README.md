# Frappe and ERPNext Installation Guide
A complete step-by-step guide to installing **Frappe** and **ERPNext** on Ubuntu, Mac, and using Windows WSL (Windows Subsystem for Linux).


Let's Start



## Table of Contents
- [Requirements](#requirements)
- [Installation Steps](#installation-steps)
- [Installing ERPNext](#installing-erpnext)
- [SEO Optimization](#seo-optimization)

## Requirements

- Ubuntu or Mac operating system (or Windows with WSL)
- Basic knowledge of terminal commands
- Internet connection for downloading packages

## Installation Steps

### Step 1: Add the Python 3.11 PPA

```bash
sudo add-apt-repository ppa:deadsnakes/ppa -y
sudo apt update
```

### Step 2: Install Python 3.11

```bash
sudo apt install python3.11
python3.11 --version  # Verify installation
```

### Step 3: Install Python 3.11 Full

```bash
sudo apt install python3.11-full
```

### Step 4: Install Git

```bash
sudo apt-get install git
```

### Step 5: Install Python Development Tools

```bash
sudo apt-get install python3-dev
```

### Step 6: Install Pip and Setuptools

```bash
sudo apt-get install python3-setuptools python3-pip
```

### Step 7: Set Up a Python Virtual Environment

```bash
sudo apt install python3.11-venv
```

### Step 8: Install MariaDB

```bash
sudo apt-get install software-properties-common
sudo apt install mariadb-server
sudo mysql_secure_installation
```
- When prompted for the root password, press ENTER if not set.
- Switch to unix_socket authentication: `Y`
- Change the root password: `Y`
- Remove anonymous users: `Y`
- Disallow root login remotely: `Y`
- Remove test database: `Y`
- Reload privilege tables: `Y`

### Step 9: Install MySQL Development Libraries

```bash
sudo apt-get install libmysqlclient-dev
```

### Step 10: Update MariaDB Configuration

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

Add the following configuration under `[server]` and `[mysql]` sections:

```ini
[server]
user = mysql
pid-file = /run/mysqld/mysqld.pid
socket = /run/mysqld/mysqld.sock
basedir = /usr
datadir = /var/lib/mysql
tmpdir = /tmp
lc-messages-dir = /usr/share/mysql
bind-address = 127.0.0.1
query_cache_size = 16M
log_error = /var/log/mysql/error.log

[mysqld]
innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci      

[mysql]
default-character-set = utf8mb4
```
Now press (Ctrl-X) to exit
Restart the MariaDB service:

```bash
sudo service mysql restart
```

### Step 11: Install Redis

```bash
sudo apt-get install redis-server
```

### Step 12: Install Node.js and NVM (Node Version Manager)

```bash
sudo apt install curl 
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
source ~/.profile
nvm install 18
node --version
```

### Step 13: Install Yarn and NPM

```bash
sudo apt-get install npm
sudo npm install -g yarn
```

### Step 14: Install wkhtmltopdf

```bash
sudo apt-get install xvfb libfontconfig wkhtmltopdf
```

### Step 15: Install Frappe Bench

```bash
sudo apt install python3-venv
python3 -m venv frappe-bench-env
source frappe-bench-env/bin/activate
pip3 install frappe-bench
bench --version
```

### Step 16: Initialize Frappe Bench

```bash
bench init frappe-bench --frappe-branch version-15 --python python3.11
cd frappe-bench/
bench start
```

Congratulations! Frappe is now installed.

## Installing ERPNext on Frappe

### Step 1: Create a New Frappe Site

```bash
bench new-site [your-site-name]
bench --site [your-site-name] add-to-hosts
```

### Step 2: Get and Install ERPNext

```bash
bench get-app erpnext --branch version-15
# OR
bench get-app https://github.com/frappe/erpnext --branch version-15

bench --site [your-site-name] install-app erpnext
bench start
```

GoodLuck Enjoy ERPNEXT
