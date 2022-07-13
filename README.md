```sh
# clone bancho.py's repository
git clone https://github.com/osuAkatsuki/bancho.py

# enter bancho.py's new directory
cd bancho.py

# clone bancho.py's dependencies' repositories
git submodule update --init
```
```sh
sudo add-apt-repository ppa:deadsnakes

# install required programs for running bancho.py
sudo apt install python3.9-dev python3.9-distutils \
                 cmake build-essential \
                 mysql-server redis-server \
                 nginx certbot

# install python's package manager, pip
wget https://bootstrap.pypa.io/get-pip.py
python3.9 get-pip.py && rm get-pip.py

# make sure pip and setuptools are up to date
python3.9 -m pip install -U pip setuptools

# install bancho.py's python-specific dependencies
python3.9 -m pip install -r requirements.txt
```
```sh
# login to mysql's shell with root - the default admin account
mysql -u root -p
```
```sql
# create a database for bancho.py to use
CREATE DATABASE YOUR_DB_NAME;

# create a user to use the bancho.py database
CREATE USER 'YOUR_DB_USER'@'localhost' IDENTIFIED BY 'YOUR_DB_PASSWORD';

# grant the user full access to all tables in the bancho.py database
GRANT ALL PRIVILEGES ON YOUR_DB_NAME.* TO 'YOUR_DB_USER'@'localhost';

# make sure privilege changes are applied immediately.
FLUSH PRIVILEGES;

# exit the mysql shell, back to bash
quit
```
```sh
# import bancho.py's mysql structure to our new db
mysql -u YOUR_DB_USER -p YOUR_DB_NAME < migrations/base.sql
```
```sh
# copy the example nginx config and make a symbolic link
sudo cp ext/nginx.conf /etc/nginx/sites-available/bancho.conf
sudo ln -s /etc/nginx/sites-available/bancho.conf /etc/nginx/sites-enabled/bancho.conf

# now, you can edit the config file.
# the spots you'll need to change are marked.
sudo nano /etc/nginx/sites-available/bancho.conf

# reload config from disk
sudo nginx -s reload
```
```sh
# create a configuration file from the sample provided
cp .env.example .env

# you'll want to configure *at least* DB_DSN (the database connection url),
# as well as set the OSU_API_KEY if you need any info from osu!'s v1 api
# (e.g. beatmaps).

# open the configuration file for editing
nano .env
```
```sh
# start the server
./main.py
```
![tada](https://cdn.discordapp.com/attachments/616400094408736779/993705619498467369/ld-iZXysVXqwhM8.png)
