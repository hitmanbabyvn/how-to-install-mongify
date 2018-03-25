# Install cac tool de compile
yum groupinstall "Development Tools"
yum -y install nano wget gdbm-devel libdb4-devel libffi-devel libyaml libyaml-devel ncurses-devel openssl-devel readline-devel tcl-devel zlib-devel  mysql-devel

2. Install ruby
wget https://cache.ruby-lang.org/pub/ruby/2.5/ruby-2.5.0.tar.gz
tar -xzvf ruby-2.5.0.tar.gz
cd ruby-2.5.0.tar
./configure
make
make install / make uninstall / make -n install

gem install mongify
gem install mysql2
gem install activerecord-mysql2-adapter
gem list --local
* activemodel (4.2.10) (remove 5.x.x version)
* activerecord (4.2.10) (remove 5.x.x version)
* activesupport (4.2.10) (remove 5.x.x version)

*try to run if something go wrong
* gem install rails -v 5.1 (choose version)
* gem install bundler

3. Install mongo 3.2 (cac ban sau bi loi ko conver duoc)
nano /etc/yum.repos.d/mongo-org-3.2.repo
[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.2.asc

yum install mongodb-org

4. Thuc hien convert

cd /root
nano database.config

sql_connection do
  adapter   "mysql"
  host      "localhost"
  username  "root"
  password  "passw0rd"
  database  "my_database"
end

mongodb_connection do
  host      "localhost"
  database  "my_database"
end

mongify check database.config
mongify translation database.config > translate.rb
mongify process database.config translate.rb
