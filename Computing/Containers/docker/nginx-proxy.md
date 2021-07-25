# nginx-proxy

```docker run --detach \
    --name nginx-proxy \
    --publish 80:80 \
    --publish 443:443 \
    --volume certs:/etc/nginx/certs \
    --volume vhost:/etc/nginx/vhost.d \
    --volume html:/usr/share/nginx/html \
    --volume /var/run/docker.sock:/tmp/docker.sock:ro \
    --net web \
    nginxproxy/nginx-proxy```

```docker run --detach \
    --name nginx-proxy-acme \
    --volumes-from nginx-proxy \
    --volume /var/run/docker.sock:/var/run/docker.sock:ro \
    --volume acme:/etc/acme.sh \
    --env "DEFAULT_EMAIL=ryan@ryanl.co.uk" \
    --net web \
    nginxproxy/acme-companion```

`docker run --detach \
    --name web-ryanl \
    --env "VIRTUAL_HOST=ryanl.co.uk,www.ryanl.co.uk" \
    --env "LETSENCRYPT_HOST=ryanl.co.uk,www.ryanl.co.uk" \
    --net web \
    web-ryanl`

`docker run --detach \
    --name web-notes-ryanl \
    --env "VIRTUAL_HOST=notes.ryanl.co.uk" \
    --env "LETSENCRYPT_HOST=notes.ryanl.co.uk" \
    --net web \
    web-notes-ryanl`


`docker run --detach \
    --name web-ryanl \
    --env "VIRTUAL_HOST=ryanl.co.uk,www.ryanl.co.uk" \
    --env "LETSENCRYPT_HOST=ryanl.co.uk,www.ryanl.co.uk" \
    --rm \
    --net web \
    web-ryanl`

`docker run --detach \
    --name web-2kanna \
    --env "VIRTUAL_HOST=2kanna.org,www.2kanna.org" \
    --env "LETSENCRYPT_HOST=2kanna.org,www.2kanna.org" \
    --rm \
    --net web \
    web-2kanna`


`docker run --net web -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro jwilder/nginx-proxy`
