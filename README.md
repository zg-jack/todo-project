# To Do List web application using Spring Boot and MySQL

A simple Todo list application using Spring Boot with the following options:

* Spring JPA and MySQL for data persistence
* Thymeleaf templae for the rendering

Follow the below steps to run the sample:

## Configure Mysql

1. Create a database in your MySQL instance.
2. Update the application.properties file in the src/main/resources folder with the URL, username and password for your MySQL instance. The table schema for the Todo objects will be created for you in the database.

## Build Docker Image
Assume you already have Docker and Maven installed.

First, clone the project and build locally:

~~
git clone https://github.com/yangzhares/mysql-spring-boot-todo.git
cd mysql-spring-boot-todo
mvn clean package docker:build
~~

## Run MySQL Container:

~~
docker run --name mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=tododb -e MYSQL_USER=user -e MYSQL_PASSWORD=pass -d mysql:5.6
~~

Check the log to make sure the server is running OK:
~~
docker logs mysql
~~

## Run Todo Container
Run todo application in Docker container and link to `mysql`:

~~
docker run -p 8080:8080 --name todo --link mysql -d zhanyang/todo-demo:1.0.0
~~

You can check the log by
~~
docker logs todo
~~

Open http://localhost:8080 in browser and add and update tasks, you can verify the changes in the database through the MySQL console:

1. `docker exec -ti mysql bash`
2. `mysql -uuser -p`
3. After login Mysql console, `use tododb;`
4. Verify tasks change status with `select category,IF(complete, 'true','false') complete,name from todo_item;`
