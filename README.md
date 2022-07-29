# Simple php-nginx hello world application

This repo has the nessecary files for a simple hello world application using php8.1-fpm and the latest nginx.


## Requirments for this app in any OS

You need to have install docker, docker-compose git and internet conection.


## installation and use

The installation steps are the following (please check the requirment above before you continue):

1. Download the repo in the folder that you want git clone `https://github.com/emakrygiannakis/webserver-php-nginx` .
2. Move into the folder of the webserver 
```bash
cd nginx-php-webserver
```
3. Create a new env file using the example.
```bash
cp .env.example .env
```
4. The variables can be changed in the file .env 
(important: If you don't know how to exit vim please use a different editor ;) )
```bash
vim .env 
```
5. Specific operator system
   If you are using linux or mac the in the env file the location needs to be like this `VOL_SRC=./www`. 
   If you are using a windows machine you need to have it like this `VOL_SRC=www`.
   If you application needs specific rights you need to edit the folder www accordintly.
6. Add the files for the php application inside the folder `www/public_html`.
7. After you finish with your configuration, you can start the container using the following command, inside the folder that has the docker-compose.yml.
```bash
docker-compose up -d 
```
8. You can access the app either using a browser by typing http://localhost/hello or using the curl command. The out of the curl will be something like:
```bash
❯ curl localhost/hello -v
*   Trying 127.0.0.1:80...
* Connected to localhost (127.0.0.1) port 80 (#0)
> GET /hello HTTP/1.1
> Host: localhost
> User-Agent: curl/7.79.1
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx
< Date: Fri, 29 Jul 2022 19:41:30 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< fastcgi_cache_result: BYPASS
< 
* Connection #0 to host localhost left intact
Hello world!%   
```
If you change the port in env for http then you need to adjust your curl by giving that port in the following example the user has the port 81.
```bash
curl localhost:81/hello -v
```
8. if you want to stop the services of the container you can do it using the following command, inside the folder that has the docker-compose.yml.
```bash
docker-compose down
```


## Usefull commands
- If  you need to access the logs of each container.
```bash
docker logs container-name
```
- If  you need to access the command line of the container.
```bash
docker exec -it container-name bash
```
- If you want to see the container that are running in the host that you are using:
```bash
docker ps
```
