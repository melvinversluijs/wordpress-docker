# Wordpress dev environment using Docker

A docker setup for wordpress development.

## Requirements

- Docker: https://docs.docker.com/engine/installation/#supported-platforms
- Wordpress: You should be able to provide your own clean Wordpress installation. (Since this build uses PHP version 7.2 only Wordpress version 4.9.3 or higher is supported.).

Make sure you got both Docker: `docker -v` and docker-compose: `docker-compose -v`

## Usage

1. Navigate to the root of this project.
2. Add your Wordpress installation and name the folder containing your Wordpress files as `wordpress`. (If you want to call it anything else please also change this on line 6 and 14 of the docker-compose.yml file).
3. Add the following line to your hosts file: `127.0.0.1 wordpress-dev.local`
4. Build the project with `docker-compose build`
   - Make sure you Use Linux containers (Windows only)
   - Execute commands in CMD as administrator (Windows only)
5. For performance reasons you should replace the nginx and php volume with the directory you are actively editing i.e. your theme folder during development. (Instead of the entire Wordpress directory).
6. Start the services by using `docker-compose up` you can add the -d option to run the services in the background.
7. Use `docker ps` to check the status of the current active containers.

```text
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
17c3489b2845        nginx:latest        "nginx -g 'daemon of…"   9 seconds ago       Up 8 seconds        0.0.0.0:80->80/tcp                  wordpress_nginx_1
634dcae84ec0        wordpress_php       "docker-php-entrypoi…"   10 seconds ago      Up 9 seconds        9000/tcp                            wordpress_php_1
9c5cf2b75a8a        mysql:8.0           "docker-entrypoint.s…"   10 seconds ago      Up 9 seconds        0.0.0.0:3306->3306/tcp, 33060/tcp   wordpress_db_1
```

8. You can use bash commands within a container by using `docker exec -ti <CONTAINER_NAME> bash` (CONTAINER_ID instead of CONTAINER_NAME will also work)
9. You can stop the containers by using `docker-compose stop`. Or stop a specific container by using `docker stop <CONTAINER_NAME>`
10. To access the Wordpress site in your browser use **wordpress-dev.local** as url. Note on MacOS the .local extension should be bypassed in the proxy settings. (Settings -> Network -> Advanced -> Proxies -> add `*.local` in the text area).
11. During the Wordpress installation step, use the following credentials for your Database:
    1. Database Name: wordpress
    2. Username: wordpress
    3. Password: wordpress
    4. Database Host: db:3306

## Using xDebug

The xdebug php extension has been added to the php container for debugging purposes. To use the debugger you should listen to port **9001**. You should map your local wordpress folder to the /code folder on the container.

In VSCode the launch.json configuration will look as follows:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for XDebug",
      "type": "php",
      "request": "launch",
      "port": 9001,
      "pathMappings": {
        "/code": "${workspaceRoot}/wordpress"
      }
    }
  ]
}
```
