1. ssh key setup for gitLab 
2. From InformationWorks: clone **TeachMoreWeb** project (I clone it in ~/WorkZone)
3. Install _bundle_ gem by: `gem install bundle`
4. Install all required _gems_ for project by: `bundle install` (required gem's list gets from _gemfile_)
5. _Step 4_ did not include _graphviz_, to  do that: `gem install graphviz`
6. To access Production database, add your ssh key to prduction server 
7. Backup and Restore Production database :
  - *SSH to teachmore.in and take a backup of the database*
```
$ ssh deployer@teachmore.in
$ cd ~/temp/db-backups
$ pg_dump postgresql://teachmoredbadmin:<PASSWORD>@teachmore-db-cluster-do-user-2900621-0.db.ondigitalocean.com:25060/teachmoredbprd?sslmode=require -f teachmore-db-backup-<DD-MMM-YYYY>.pgsql
```
  - *Execute below commands on your local development machine*
```
# We will copy the backup file from server to our machine and then restore the file using "teachmoredbadmin" user.
# If "teachmoredbadmin" is not created on your machine, open PgAdmin and create that user as superuser and provide all permissions to the user.
$ cd /your/rails/project/folder/path/
$ rails db:drop
$ rails db:create
$ cd ~/temp/db-backups/
$ scp deployer@teachmore.in:/home/deployer/temp/db-backups/teachmore-db-backup-<DD-MMM-YYYY>.pgsql ./teachmore-db-backup-<DD-MMM-YYYY>.pgsql
$ psql -U teachmoredbadmin -d teachmore_dev < teachmore-db-backup-24-Nov-2018.pgsql
 
# Once database is restored, delete all entries from devices table so we don't end up sending push notifications by mistake.
$ rails c
:001:0> Device.delete_all
```
8. install **_pgsql_** 
  - `$ sudo apt install postgresql postgresql-contrib` to install PostgreSQL
  - The installation procedure created a user account called postgres that is associated with the default Postgres role. In order to use Postgres, you can log into that account.
  - Switch over to the postgres account on your server by typing: `$ sudo -i -u postgres` 
  - You can now access a Postgres prompt immediately by typing: `$ psql`
  - Exit out of the PostgreSQL prompt by typing: `\q`
  - If you are logged in as the postgres account, you can create a new user by typing: `$ createuser --interactive`
  - Output:
  	```
    Enter name of role to add: user_name
	Shall the new role be a superuser? (y/n) y
	```
9. Setup _ pgAdmin lll _ to disply database
