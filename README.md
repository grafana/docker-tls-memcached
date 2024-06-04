# How to build the image

1- Clone the repo

``` bash
git clone git@github.com:grafana/docker-tls-memcached.git
```

2- Go to the `certs` folder, clean and regenerate the certs

``` bash
cd docker-tls-memcached/certs
make clean 
make all
```

3- Go back to the project root folder and build a docker image

``` bash
cd ..
docker build . -t memcached-tls-local -f ./debian/Dockerfile
```

4- Run memcached with the newly created image. You can add `-vv` at the end of it for detailed logs

``` bash
docker run -p 11211:11211 memcached-tls-local 
```