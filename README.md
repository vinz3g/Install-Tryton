# Install-Tryton

Antes de instalar
modificar 

/etc/bash.bashrc
```
sudo nano /etc/bash.bashrc
```
```
if [ -d "$HOME/.local" ] ; then
PATH="$HOME/local:$PATH"
fi
```
Installing tryton(d) 5.2* on ubuntu 18.04.3 with postgres 11 for newbys by newby
since it took me a while to get tryton running. i want to chair the steps i took.

install tryton 5.2.* on ubuntu 18.04.3 with postrges 11 for newbys by newby
```
install ubuntu 18.04.3
```
```
download ubuntu 26
```
open terminal

```
crtl + alt + t
```
```
sudo apt-get update

```
sudo apt-get upgrade
```

```
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

~~sudo apt update && sudo apt -y upgrade
sudo reboot
sudo apt install -y wget

~~wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo tee /etc/apt/sources.list.d/pgdg.list <<END deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main END
sudo apt update
sudo apt -y install postgresql-11
sudo systemctl start postgresql@11-main


~~sudo nano /etc/postgresql/11/main/postgresql.conf

```
sudo nano /etc/postgresql/14/main/postgresql.conf
```

add line to conf file by connention settings

```
listen_addresses = '*'
```
```
sudo systemctl restart postgresql
```

~~sudo ufw allow 5432/tcp

```
sudo apt-get install python-psycopg2 libpq-dev python3-psycopg2
```

create database
```
sudo -u postgres psql
```
```
CREATE DATABASE tryton_test WITH OWNER = postgres ENCODING = 'UTF8' LC_COLLATE = 'C' LC_CTYPE = 'C' TABLESPACE = pg_default CONNECTION LIMIT = -1 TEMPLATE template0;
```

create role
```
CREATE ROLE tryton_test WITH LOGIN NOSUPERUSER NOCREATEDB NOCREATEROLE INHERIT NOREPLICATION CONNECTION LIMIT -1 PASSWORD 'tryton_test';
```
postgres=#
```
\q
```

make trytond.config
```
sudo mkdir /etc/tryton
```
```
sudo nano /etc/tryton/trytond.conf
```
past: (sorry don’t remeber the source)

```
# /etc/tryton/trytond.conf - Configuration file for Tryton Server (trytond)
 #
 # This file contains the most common settings for trytond (Defaults
 # are commented).
 # For more information read
 # /usr/share/doc/trytond-<version>/

 [database]
 # Database related settings

 # The URI to connect to the SQL database (following RFC-3986)
 # uri = database://username:password@host:port/
 # (Internal default: sqlite:// (i.e. a local SQLite database))
 #
 # PostgreSQL via Unix domain sockets
 # (e.g. PostgreSQL database running on the same machine (localhost))
 #uri = postgresql://tryton:tryton@/
 #
 #Default setting for a local postgres database
 #uri = postgresql:///

 #
 # PostgreSQL via TCP/IP
 # (e.g. connecting to a PostgreSQL database running on a remote machine or
 # by means of md5 authentication. Needs PostgreSQL to be configured to accept
 # those connections (pg_hba.conf).)
 #uri = postgresql://tryton:tryton@localhost:5432/
 uri = postgresql://tryton_test:tryton_test@localhost:5432/

 # The path to the directory where the Tryton Server stores files.
 # The server must have write permissions to this directory.
 # (Internal default: /var/lib/trytond)
 path = /var/lib/tryton

 # Shall available databases be listed in the client?
 #list = True

 # The number of retries of the Tryton Server when there are errors
 # in a request to the database
 #retry = 5

 # The primary language, that is used to store entries in translatable
 # fields into the database.
 language = nl
 # en

 [ssl]
 # SSL settings
 # Activation of SSL for all available protocols.
 # Uncomment the following settings for key and certificate
 # to enable SSL.

 # The path to the private key
 #privatekey = /etc/ssl/private/ssl-cert-snakeoil.key

 # The path to the certificate
 #certificate = /etc/ssl/certs/ssl-cert-snakeoil.pem

 [jsonrpc]
 # Settings for the JSON-RPC network interface

 # The IP/host and port number of the interface
 # (Internal default: localhost:8000)
 #
 # Listen on all interfaces (IPv4)

 listen = 0.0.0.0:8000

 #
 # Listen on all interfaces (IPv4 and IPv6)
 #listen = [::]:8000

 # The hostname for this interface
 #hostname =

 # The root path to retrieve data for GET requests
 #data = jsondata

 [xmlrpc]
 # Settings for the XML-RPC network interface

 # The IP/host and port number of the interface
 #listen = localhost:8069

 [webdav]
 # Settings for the WebDAV network interface

 # The IP/host and port number of the interface
 #listen = localhost:8080
 listen = 0.0.0.0:8080

 [session]
 # Session settings

 # The time (in seconds) until an inactive session expires
 timeout = 3600

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
 --------------------------------------------
 
 initialize database
 ```
trytond-admin -c /etc/tryton/trytond.conf -d tryton_test --all
```
“admin” email for “tryton_test”: YOURMAIL@YOUKNOWHAT.COM
“admin” password for “tryton_test”: snafu
“admin” password confirmation: snafu
—>

run trytond
```
trytond -c /etc/tryton/trytond.conf
```

run tryton client
tryton
Host: localhost
Database: tryton_test
username: admin

password: snafu
 
 
******** Fuente: https://discuss.tryton.org/t/installing-tryton-d-5-2-on-ubuntu-18-04-3-with-postgres-11-for-newbys-by-newby/1809 *****
