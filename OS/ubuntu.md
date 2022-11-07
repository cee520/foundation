---
cover: >-
  https://images.unsplash.com/photo-1519389950473-47ba0277781c?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2970&q=80
coverY: 0
---

# Ubuntu

{% hint style="info" %}
**Good to know:** an employee directory can be a great way to help new folks get familiar with everyone they're going to be working with.
{% endhint %}

## Install Env

### RVM

```
https://rvm.io

gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io -o rvm_install.sh
bash rvm_install.sh

```

### Ruby

```
rvm install ruby-3.1.2
rvm use 3.1.2
rvm gemset create r703

```

### Rust

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Docker

<pre><code>sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
<strong># add Docker's official GPG key:
</strong><strong>sudo mkdir -p /etc/apt/keyrings
</strong>curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg    
# Set up the repository:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null</code></pre>

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

```



### Node.js

```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get update
sudo apt install nodejs

```

### Yarn

```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update

sudo apt install yarn

yarn config set registry https://registry.npm.taobao.org/
yarn config get registry
```

### **Redis**

```
docker pull redis

docker run --name myredis -d redis
docker exec -it myredis redis-cli

```

### **Postgres**

Docker Install&#x20;

```
docker search postgres
docker pull postgres
# Startup
docker run --name mypostgres -d -p 5432:5432 -e POSTGRES_PASSWORD=123456 postgres
# enter contanter
docker exec -it mypostgres psql -U postgres -d postgres
# connect
psql -U username -h ipaddress -d dbname
select * from pg_tables;

```

Ubuntu Install

```
# Install Postgres dev
# Create the file repository configuration:
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Import the repository signing key:
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update the package lists:
sudo apt-get update

sudo apt install postgresql-12
sudo apt install libpq-dev

sudo -u postgres sql
```

###

### qBittorrent qbittorrent.org ****&#x20;

****

****
