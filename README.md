# mixpost_docker

A [Mixpost](https://github.com/inovector/mixpost) Installation with Docker Containers.


## Set environments values

Create all the environments values for the **Mixpost** service, executing the following commands:

```
cp .env.example .env
nano .env
```

Checkout the meaning for the environments variables:

* ``MIXPOST_APP_NAME``, Mixpost project name. Default value: ``Mixpost``.

* ``MIXPOST_APP_URL``, Mixpost App Url, like ``http://localhost``.

* ``MIXPOST_APP_PORT``, Mixpost App Port, like ``9000``.

* ``MIXPOST_APP_KEY``, Mixpost App Laravel Key, generate a base64 secret here: https://generate-random.org/laravel-key-generator?count=1.

* ``MIXPOST_APP_ENV``, Mixpost App Enviroment, available options: ``local``/``production``/``testing``. Default value: ``production``.

* ``MIXPOST_APP_DEBUG``, Mixpost Debug option, available options: ``true``/``false``. Default value: ``false``.

* ``MIXPOST_DB_HOST``, The IP and port of the linked ``mysql`` container. Default value: ``mysql``.

* ``MIXPOST_DB_DATABASE``, Mixpost database name of the linked ``mysql`` container, like ``mixpost``.

* ``MIXPOST_DB_USERNAME``, Mixpost user name, this user of the linked ``mysql`` container, don't use the name with spaces (temporary issue).

* ``MIXPOST_DB_PASSWORD``, Mixpost user password, this user password of the linked ``mysql`` container.

* ``MIXPOST_REDIS_HOST``, The IP and port of the linked ``redis`` container. Default value: ``redis``.

* ``MIXPOST_REDIS_PASSWORD``, Redis password, the redis password of the linked ``redis`` container.

Replace the ``CHANGE_ME_HERE`` values for the real value and save the ``.env`` file.


## Install

For install the containers, executing the following command:


### Create network

Create a Docker network as external for mixpost container, executing the following command:

```
docker network create mixpost_net
```


### Run containers

Pull the images and run the containers, executing the following command:

```
docker-compose up -d
```


### Log mixpost container

An admin user will be created automatically. Check the mixpost container logs to find out the password, executing the following command:

```
docker-compose logs -f mixpost
```


## Run migrations

Once you have installed Mixpost using Docker, you can run database migrations.
For run the database migrations, executing the following command:

```
docker-compose exec -it mixpost bash -c "php artisan migrate"
```


## Create new user

Once you have ran the Mixpost database migrations, you can create a new user.

Log in to Mixpost container, executing the following command:

```
docker-compose exec -it mixpost bash -c "php artisan mixpost-auth:create"
```

The previous command make some questions to you for the user creation, executing the following command:

```
 What is the name of the new user?:
 > administrator

 What is the email address of the new user?:
 > administrator@yoursite.com

 What is the password for the new user?:
 > 1234567890

User administrator@yoursite.com created successfully!
```


## Change user password

Once you have created a Mixpost username, you can change the user password.

Log in to Mixpost container, executing the following command:

```
docker-compose exec -it mixpost bash -c "php artisan mixpost-auth:password administrator@yoursite.com"
```

The previous command make a question to you for the change the user password:

```
 What is the new password?:
 >

Password for administrator@yoursite.com updated successfully!
```


## Log in to Mixpost container

You can log in to Mixpost container, executing the following command:

```
docker-compose exec -it mixpost bash
```

For exit from Mixpost container, executing the following command:

```
exit
```


## Use it

Later that you create a new user, you can access to the <http://localhost:9000/mixpost> URL and enter the user and password for login.


## Conclusion

Docker is a powerful tool for managing applications in containers. By following the steps outlined in this guide, you can easily install and manage Mixpost using Docker.
