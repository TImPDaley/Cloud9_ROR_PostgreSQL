         ___        ______     ____ _                 _  ___  
        / \ \      / / ___|   / ___| | ___  _   _  __| |/ _ \ 
       / _ \ \ /\ / /\___ \  | |   | |/ _ \| | | |/ _` | (_) |
      / ___ \ V  V /  ___) | | |___| | (_) | |_| | (_| |\__, |
     /_/   \_\_/\_/  |____/   \____|_|\___/ \__,_|\__,_|  /_/ 
 ----------------------------------------------------------------- 


THIS IS A RUBY ON RAILS with PostgreSQL CLOUD 9 Deveopment machine on AWS Template

To get started, create a new application ($rails new ... ) and play with the terminal,
or visit https://docs.aws.amazon.com/console/cloud9/ for our documentation.

# Updates to system

RUN these commands

```
$ sudo apt update

$ sudo apt upgrade

$ rvm get stable

$ rvm reload

$ rvm install ruby-3.2.1

$ rvm --default use 3.2.1

$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.6 LTS
Release:        18.04
Codename:       bionic

$ ruby -v
ruby 3.2.1 (2023-02-08 revision 31819e82c8) [x86_64-linux]

gem update --system

gem pristine

gem install bundler

gem install rails

$ node --version
v16.19.1

# May need to install node and update nvm... Looks like I'm OK

```

## Now install Heroku Tool Belt (if you plan on deploying to Heroku)

```
$ sudo snap install --classic heroku
heroku v7.60.1 from Heroku✓ installed
$ sudo snap refresh heroku
snap "heroku" has no updates available

```

### NOTE 
- Login to Heroku with 'heroku login -i' command enter username and password

# Install PostgreSQL
https://phoenixnap.com/kb/how-to-install-postgresql-on-ubuntu

```
$ sudo apt-get install wget ca-certificates
Reading package lists... Done
Building dependency tree       
Reading state information... Done
ca-certificates is already the newest version (20211016ubuntu0.18.04.1).
wget is already the newest version (1.19.4-1ubuntu2.2).
wget set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
OK

$sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" &gt; /etc/apt/sources.list.d/pgdg.list'

$ sudo apt-get update

$ sudo apt-get install postgresql postgresql-contrib

# NOW CONNECT 

$ sudo su - postgres
postgres@ip-172-31-73-72:~$ psql
psql (10.23 (Ubuntu 10.23-0ubuntu0.18.04.1))
Type "help" for help.

postgres=# 
postgres=# \conninfo
You are connected to database "postgres" as user "postgres" via socket in "/var/run/postgresql" at port "5432".

```
### Now you need to setup users in the database....

```
$ sudo su - postgres
postgres@ip-172-31-73-72:~$ psql
psql (10.23 (Ubuntu 10.23-0ubuntu0.18.04.1))
Type "help" for help.

postgres=# 
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

postgres=# CREATE USER ubuntu WITH PASSWORD '<PASSWORD>';
CREATE ROLE
postgres=# ALTER USER ubuntu WITH SUPERUSER;
ALTER ROLE

postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 ubuntu    | Superuser                                                  | {}

postgres=# 
postgres=# \q
postgres@ip-172-31-73-72:~$ exit
logout
```

# post install notes 

had to run this command for bundle install to work???

```
$sudo apt-get install libpq-dev
```
UPDATE bundler 
```
$ gem update --system 3.2.3
```

- Getting error about yarn out of date... 
- yarn install --check files