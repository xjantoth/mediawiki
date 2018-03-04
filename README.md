
## Hwo to use this Docker image


#### at your local filesystem delete ../data folder

```
# this location is basically "sqlite database storage"

cd /opt/mediawiki
rm -rf data/*
mv www/mediawiki/LocalSettings.php www/mediawiki/LocalSettings.php.orig


```



#### Note
```
docker image prune -a
WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
Deleted Images:
 ...
```

#### pull docker images from docker hub

```
docker login
...
...
docker pull jantoth/mediawiki:v1

docker images

jantoth@ubuntu-ansible:/opt/mediawiki$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
jantoth/mediawiki   v1                  5d0f4242fd0b        3 weeks ago         307MB

```

#### Run your image 

```bash
jantoth@ubuntu-ansible:/opt/mediawiki$ docker run --name mediawiki_1 -d \
                                                  -v "/opt/mediawiki/nginx":/etc/nginx:ro \
                                                  -v "/opt/mediawiki/www":/var/www:rw \
                                                  -v  /opt/mediawiki/data:/var/lib/nginx/data:rw  \
                                                  -p 7000:7000 \
                                                  -p 10400:10400 \ 
                                                  jantoth/mediawiki:v1
                                                  
331dfc8d9ef62034e5927621659bd89fb4538db87c977c09c265da02bcb34ea0
```

#### Chcek if your image is up and running


```bash
jantoth@ubuntu-ansible:/opt/mediawiki$ docker ps
CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                                              NAMES
331dfc8d9ef6        jantoth/mediawiki:v1   "/usr/bin/supervis..."   5 seconds ago       Up 3 seconds        0.0.0.0:7000->7000/tcp, 0.0.0.0:10400->10400/tcp   mediawiki_1

```

#### Login via web interface

My nging is configured with a domain name so I am taking
advantage out of it.

```
http://scaleway.linuxinuse.com:10400/mediawiki/
```







