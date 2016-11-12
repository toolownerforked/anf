# ANF Base Image

Nginx build on Alpine with FastCGI.

# Run

### Test Server

If your host is `example.com` and port is `9090` here's how to run a simple test:

    docker run -p 9090:80 -h example.com --name anf-server -d aquaron/anf

Point your browser to `example.com:9090` you should see a simple message with a link.
Click on that to see the CGI in action.

### Enter the Container

To run the Nginx server manually:

    docker run -it -p 9090:80 --name anf-server --entrypoint=/bin/sh aquaron/anf

Once inside the container:

	runme.sh test


### Start Server

You need to map 3 local paths to the container's:
    <datadir>  - the root of the server
    <logdir>   - where the server log will be written 
    <etcdir>   - stores the conf

`<port>` is local port to foward to the server's `8080` port.
`--name` directive gives the container the name for ease of access, in this example,
we give it `anf-server` as the name of the container.
`-d` tells `docker` to detatch the container.

    docker run -p <port>:80 \
        -h <hostname> \
        -v <datadir>:/usr/share/nginx \
        -v <logidr>:/var/log/nginx \
        -v <etcdir>:/etc/nginx \
        --name anf-server \
        -d aquaron/anf

### Stop Server

    docker stop anf-server

### Remove the Container

    docker rm anf-server

### Remove Image

    docker rmi aquaron/anf
    

### Create Container & Run

    docker create -p <port>:80 \
        -h <hostname> \
        -v <datadir>:/usr/share/nginx \
        -v <logidr>:/var/log/nginx \
        -v <etcdir>:/etc/nginx \
        --name anf-server \
        aquaron/anf

    docker start anf-server

