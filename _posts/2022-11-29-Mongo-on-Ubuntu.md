---
layout: post
title: Mongo Installation
author: Uttam Jaiswal
date: 2022-11-29
categories: Ubuntu Mongodb
---
# MongoDB installation on Ubuntu

```
sudo apt update
sudo apt install wget curl gnupg2 software-properties-common apt-transport-https ca-certificates lsb-release

curl -fsSL https://www.mongodb.org/static/pgp/server-5.0.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/mongodb.gpg

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list

sudo apt update
sudo apt install mongodb-org

sudo systemctl enable mongod
sudo systemctl restart mongod
```

Create a user:
```
db.createUser({user: "root", pwd: "xxxxxxxxxx", roles : [{"role" : "backup","db" : "admin"}, {"role" : "clusterMonitor","db" : "admin"}, {"role" : "dbAdminAnyDatabase","db" : "admin"}, {"role" : "readAnyDatabase", "db" : "admin" }, {"role" : "readWriteAnyDatabase","db" : "admin"}, {"role" : "restore", "db" : "admin"}]})
```

Enable the desired port:
```
vi /etc/mongod.conf

net:
  port: 27917
##  bindIp: 127.0.0.1
  bindIp: 0.0.0.0

security:
  authorization: "enabled"
```

Login from terminal:
```
mongosh --port 27917

use admin
db.auth("root1","passNov30")
```
