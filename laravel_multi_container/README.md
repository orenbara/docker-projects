# Laravel Multi-Container

The environmnet includes the following containers:
NGINX, PHP-FPM-8.1, MySql, Composer(Installing Laravel), Artisan, npm

## Requirements:
Docker Engine
Docker Compose

## Instuctions For Building And Running the environmnet:
* Make sure you have /src folder, and run only the Composer container from the docker-compose.yaml file to make the source code of the application.
* sudo docker-compose run --rm composer create-project --prefer-dist laravel/laravel .
 * [LINUX] There is an issue when /src is owned by root, it is recommanded to create the project under different user.

* Change the DB section inside /src/.env acording to the ENV variables at /env/mysql.env
*The DB section should look like this if we leave the defaults(Don't leave the defalts!):
  *DB_CONNECTION=mysql
  *DB_HOST=mysql      (Please note that this is the Myql container-name here)
  *DB_PORT=3306
  *DB_DATABASE=homestead
  *DB_USERNAME=homestead
  *DB_PASSWORD=secret

* After /src is populated and .env modifed we can run the containers which suppose to stay alive: nginx, php, mysql(without artisan and npm):
  * sudo docker-compose up --build server php mysql

*[This step is optional] - Run artisan Utility container to be able to populate the DB and migrate data to it:
  *The following command will run artisan utility container and kill it after its done: sudo docker-compose run --rm artisan migrate

*[This step is optional] - Add npm container for Laravel fronend:
  * sudo docker-compose run --rm npm install      (npm here is the name if the container, "npm" entry is already inside the docker-compose file)
