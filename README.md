# cbwa_ca1
A very small Docker image (~154KB) to run any static website, based on the [BusyBox httpd](https://www.busybox.net/) static file server.

> If you're using the previous version (1.x, based on thttpd), I recommend upgrading since the new version (2.x) comes with a much smaller memory footprint.

## Usage

Code added to run ERD_TABLES from git respository:

dockerfile
RUN wget https://github.com/recarvalhoo/ERD_TABLES/archive/master.tar.gz && tar xf master.tar.gz && rm master.tar.gz && mv /ERD_TABLES-master /home/static

#copy the CA file
COPY --from=builder /home/static /home/static

## Changing working directory to /home/static/web_ca1-main
WORKDIR /home/static/ERD_TABLES-master


Build the image:

sh
docker build -t my-cloud-ca1-renata .


Run the image:

sh
docker run -it --rm -p 8080:8080 my-cloud-ca1-renata


Browse to `http://localhost:8080`.

If you need to configure the server in a different way, you can override the `CMD` line:

dockerfile

CMD ["/busybox", "httpd", "-f", "-v", "-p", "8080", "-c", "httpd.conf"]

### Referencing code used from someone else

Read the [source code comments](https://github.com/lipanski/docker-static-website).
