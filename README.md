## Build the image

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

## Configure Grafana

Run Grafana Enterprise with the following configuration in the `config.ini` file. Change `{PROJECT_FOLDER}` to the root folder location of the `docker-tls-memcached` project.

```ini
[feature_toggles]
enable = tlsMemcached

[caching]
backend= "memcached"
enabled = true

[caching.memcached]
servers = "localhost:11211"
tls-enabled = true
tls-cert-path = "`{PROJECT_FOLDER}/certs/gen/crt/client.crt"
tls-key-path = "`{PROJECT_FOLDER}/certs/gen/key/client.key"
tls-ca-path = "`{PROJECT_FOLDER}/certs/gen/crt/ca-root.crt"
tls-server-name="localhost"
```