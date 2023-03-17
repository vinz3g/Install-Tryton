# Install-Tryton
Installing tryton(d) 5.2* on ubuntu 18.04.3 with postgres 11 for newbys by newby
since it took me a while to get tryton running. i want to chair the steps i took.

install tryton 5.2.* on ubuntu 18.04.3 with postrges 11 for newbys by newby
install ubuntu 18.04.3
download ubuntu 26

open terminal
crtl + alt + t
sudo apt-get update
sudo apt-get upgrade

install pip 3
```
sudo apt-get install python3-pip
```
install tryton en tytond en tryton_sale

```
sudo apt install pkg-config
```

```
pip3 install trytond
```
```
sudo apt-get install libglib2.0-dev libgirepository1.0-dev python3-cairo libcairo2-dev
```
```
pip3 install pycairo
```
```
pip3 install tryton
```
```
`pip3 install trytond_sale’
```
installing postgres
postgres 30
```
sudo apt install postgresql postgresql-contrib
```
~~ ~~
sudo apt update && sudo apt -y upgrade
sudo reboot
sudo apt install -y wget

wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo tee /etc/apt/sources.list.d/pgdg.list <<END deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main END
sudo apt update
sudo apt -y install postgresql-11
sudo systemctl start postgresql@11-main
~~ ~~

sudo nano /etc/postgresql/11/main/postgresql.conf
add line to conf file by connention settings
listen_addresses = '*'

sudo systemctl restart postgresql
sudo ufw allow 5432/tcp
sudo apt-get install python-psycopg2
sudo apt-get install libpq-dev
sudo apt-get install python3-psycopg2

create database
sudo -u postgres psql

CREATE DATABASE tryton_test WITH OWNER = postgres ENCODING = 'UTF8' LC_COLLATE = 'C' LC_CTYPE = 'C' TABLESPACE = pg_default CONNECTION LIMIT = -1 TEMPLATE template0;

create role
CREATE ROLE tryton_test WITH LOGIN NOSUPERUSER NOCREATEDB NOCREATEROLE INHERIT NOREPLICATION CONNECTION LIMIT -1 PASSWORD 'tryton_test';

postgres=# \q

make trytond.config
sudo mkdir /etc/tryton

sudo nano /etc/tryton/trytond.conf
past: (sorry don’t remeber the source)

```
 # The server administration password used by the client for
 # the execution of database management tasks. It is encrypted
 # using using the Unix crypt(3) routine. A password can be
 # generated using the following command line (on one line):
 # $ python -c 'import getpass,crypt,random,string; \
 # print crypt.crypt(getpass.getpass(), \
 # "".join(random.sample(string.ascii_letters + string.digits, 8)))'
 # Example password with 'admin'
 #super_pwd = jkUbZGvFNeugk
 #super_pwd = <your pwd>


 [email]
 # Mail settings

 # The URI to connect to the SMTP server.
 # Available protocols are:
 # - smtp: simple SMTP
 # - smtp+tls: SMTP with STARTTLS
 # - smtps: SMTP with SSL
 #uri = smtp://localhost:25
 uri = smtp://localhost:25

 # The From address used by the Tryton Server to send emails.
 from = tryton@<your-domain.tld>

 [report]
 # Report settings

 # Unoconv parameters for connection to the unoconv service.
 #unoconv = pipe,name=trytond;urp;StarOffice.ComponentContext

 # Module settings
 #
 # Some modules are reading configuration parameters from this
 # configuration file. These settings only apply when those modules
 # are installed.
 #
 #[ldap_authentication]
 # The URI to connect to the LDAP server.
 #uri = ldap://host:port/dn?attributes?scope?filter?extensions
 # A basic default URL could look like
 #uri = ldap://localhost:389/

 [web]
 # Path for the web-frontend
 #root = /usr/lib/node-modules/tryton-sao
 listen = 0.0.0.0:8000
 root = /usr/share/sao


 [sale]
```
initialize database
trytond-admin -c /etc/tryton/trytond.conf -d tryton_test --all
“admin” email for “tryton_test”: YOURMAIL@YOUKNOWHAT.COM
“admin” password for “tryton_test”: snafu
“admin” password confirmation: snafu
—>

run trytond
trytond -c /etc/tryton/trytond.conf

run tryton client
tryton
Host: localhost
Database: tryton_test
username: admin

password: snafu

Source: https://discuss.tryton.org/t/installing-tryton-d-5-2-on-ubuntu-18-04-3-with-postgres-11-for-newbys-by-newby/1809
