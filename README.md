Docker + Wordpress
==================

1. Install Docker
----------------------

Docker only works inside a Linux environment. Mac and Windows users need to install Boot2Docker. But don't worry, once this is set up, using docker feels the same as using it locally.

### Mac Users
[Install boot2docker for Mac](http://docs.docker.com/mac/step_one/)

### Linux Users
[Install docker for Linux](http://docs.docker.com/linux/step_one/)

### Windows Users
[Install boot2docker for Windows 7.1+](http://docs.docker.com/windows/step_one/)


2. Install `docker-compose`
---------------------------

**Windows Users:** Unfortunately docker-compose isn't available for Windows yet. You'll need to manually set up your containers.

[See the official docs for instructions](https://docs.docker.com/compose/install/)

3. Create a WordPress Container
-------------------------------

1. Create a new folder in your user directory or just clone this repository.

2. Create a new file `docker-compose.yml` and enter the following:

		wordpress:
			image: wordpress
			links:
				- db:mysql
			ports:
				- 8080:80

		db:
			image: mariadb
			environment:
				MYSQL_ROOT_PASSWORD: example

3. If using boot2docker, run:

		boot2docker ip

	Copy this down, you'll need it for Step 5

4. At the terminal, run:

		docker-compose up

	Docker will then start building the image. This may take some time, but it only needs to be done once.

5. Open up the Docker VM IP address in the browser, for example

		http://<boot2docker ip>:8080

6. Install WordPress as usual!


4. Mounting a local folder
-----------------------------------------

While developing a theme or plugin you will want to be able to edit the files inside the container. In this section we'll link up a folder on the local filesystem to the server's html directory. This way we can easily edit themes and plugins with our favourite editor.

1. Create a new folder:

		mkdir src

2. Open the `docker-compose.yml` file and add a `volumes` section under the `wordpress` container

		wordpress:
			...
			volumes:
				- ./src:/var/www/html
		...

3. Once again run:

		docker-compose up

4. You can copy your themes, plugins etc. into `./src/wp-content`, or edit `./src/wp-config.php`.


5. Install WP-CLI
-----------------

In this section we will customise the image used to start new WordPress containers by installing WP-CLI. First let's have a look at official WordPress docker image.

1. Take a look at the [official WordPress Dockerfile](https://github.com/docker-library/wordpress/blob/master/apache/Dockerfile)

	If you've set up a new Linux server to host WordPress, these commands might look pretty familiar. Notice the first line:

		FROM php:5.6-apache

	This means that this Dockerfile actually builds off another Dockerfile. In this way you can set up a tree of Dockerfiles as needed.

2. Create a new folder in which we'll describe the image with WP-CLI:

		mkdir wpcli

3. Create a new file `./wpcli/Dockerfile` and fill it with the following:

		FROM wordpress

		# Install WP-CLI
		RUN apt-get update
		RUN apt-get install -y wget
		RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar -O /bin/wp
		RUN chmod +x /bin/wp

4. Inside `docker-wordpress.yml`, change the following line

		image: wordpress

	to:

		build: ./wpcli

5. Build and start the new containers

		docker-compose up

6. Now you can start a new WordPress container running a terminal:

		docker-compose run wordpress bash
		wp --allow-root post list
