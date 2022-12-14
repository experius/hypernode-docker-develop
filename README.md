
# Hypernode Docker Develop

### Container list

```
docker pull experiusnl/hypernode-buster-docker-php81-mysql80-develop-magento245-sample-data
```

coming soon
```
docker pull experiusnl/hypernode-buster-docker-php81-mysql80-develop-magento245
docker pull experiusnl/hypernode-buster-docker-php81-mysql80-develop
```

## Quick start

### Pull and run container

```
docker run -d -p 3306:3306 -p 22:22 -p 80:80 -p 443:443 -p 8025:8025 -p 9200:9200 -v <local_path>:/data/web/magento --name magento245 experiusnl/hypernode-buster-docker-php81-mysql80-develop-magento245-sample-data
```

### Copy magento files to mounted volume / folder and create new symlink

```
docker exec -u app:app magento245 bash -c 'mv /data/web/magento2/* /data/web/magento && unlink /data/web/public && ln -s /data/web/magento/pub /data/web/public'
```

### Copy ssh key to container

```
docker cp ~/.ssh/id_rsa.pub magento245:/data/web/.ssh/id_rsa_client.pub 
docker exec magento245 bash -c 'cat /data/web/.ssh/id_rsa_client.pub > /data/web/.ssh/authorized_keys'
docker exec magento245 bash -c 'cat /data/web/.ssh/id_rsa_client.pub > /root/.ssh/authorized_keys'
```

### Ssh into container
```
ssh app@127.0.0.1 -p22
```

### Xdebug ssh tunnel

```
ssh -oStrictHostKeyChecking=no -oUserKnownHostsFile=/dev/null app@localhost' -p22 -R 127.0.0.1:9005:127.0.0.1:9000
```

### Bash aliases

MageTV cache cleaner
```
cf --watch 
```

Php cli with Xdebug
```
phpx bin/magento
```

### Hypernode docker documentation
https://github.com/ByteInternet/hypernode-docker
