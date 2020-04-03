# Quick reference

 - **Where to get help**:
    https://github.com/scoriacorp/docker-tls-memcached

 - **Where to file issues**:
    https://github.com/scoriacorp/docker-tls-memcached

 - **Maintained by**:
    [Moisés Guimarães](https://github.com/moisesguimaraes)

# How to use this image

This image runs a Memcached server with TLS enabled, so it will only accept TLS requests.

The CA certificate can be extracted with:

```shell
docker run --it scoriacorp/tls_memcached cat /opt/certs/crt/ca-root.crt
```

The server's certificate Common Name (CN) is `*.localhost`, so you must use localhost:11211 when connecting to it and for now you must bind port 11211 to the host machine.

For client side authentication, trusted client credentials can be found at:

```
docker run --it scoriacorp/tls_memcached cat /opt/certs/key/client.key
docker run --it scoriacorp/tls_memcached cat /opt/certs/crt/client.crt
```