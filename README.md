# Laravel / Php / Nginx / Mysql with Docker
This project will make a Laravel environment with Nginx, Php, and Mysql easily just using docker. 

### Requirements
  - Docker
  - Composer installed (optional)

## Project setup
If you don't have Composer installed globally you can use the next command in the main folder to execute composer install. This uses a Docker image of Composer. The -v and --rm flags with "docker run" will make partial containers.
```
docker run --rm -v $(pwd):/app composer install
```
Run this command to set the user permisions
```
sudo chown -R $USER ./folder
```
Copy the .env.example and create a .env
```
cp .env.example .env
```
You can use this configuration for the .env
```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=1234
```

Then run:
```
docker-compose up -d
```

Then you have to run this command.
```
docker-compose exec app php artisan key:generate
```

## (Optional) Create a user, to do not use Root
```
docker-compose exec db bash
mysql -u root -p (default password is 1234)

mysql> show databases;
mysql> GRANT ALL ON laravel.* TO 'newUser'@'%' IDENTIFIED BY 'userPassword';
mysql> FLUSH PRIVILEGES;
mysql> exit
```
Once you created the new user change the credentials in the .env file.

## (Optional) Run Migrations
```
docker-compose exec app php artisan migrate
```

