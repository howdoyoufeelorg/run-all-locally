HowDoYouFeel.org - DOCKER-COMPOSE for the entire project
=========================

This is a docker-compose script to run the entier HowDoYouFeel.org. You need to fetch the components themselves, and place them
in a directory stucture, like so:

```bash
$ git clone git@github.com:howdoyoufeelorg/api.git  
$ git clone git@github.com:howdoyoufeelorg/admin.git
$ git clone git@github.com:howdoyoufeelorg/front.git
```

There are some additional commands you need to execute in api repo directory:

``` bash
$ cd api/
$ mkdir -p config/jwt
$ openssl genpkey -out config/jwt/private.pem -aes256 -algorithm rsa -pkeyopt rsa_keygen_bits:4096
$ openssl pkey -in config/jwt/private.pem -out config/jwt/public.pem -pubout  
```
If the systems asks for a passphrase, you need to give one - but this passphrase also needs to be set in the .env file. Or you can use the one from the .env file, it's local anyway.

You should then be able to run the project like so:

```bash
$ docker-compose build
$ docker-compose up -d
```

The first thing to do is to install composer dependencies:

```bash
$ docker-compose exec api composer install
```

Then you need to issue commands to create the database in the db container. You do this via api container doctrine commands, like so:

```bash
$ docker-compose exec api bin/console doctrine:database:create
$ docker-compose exec api bin/console doctrine:schema:create 
```

Finally, you should activate fixtures to create a test user and an initial set of questions:
 
```bash
$ docker-compose exec api bin/console doctrine:fixtures:load
```

Front should be accessible at http://localhost:3000

Admin should be accessible at http://localhost:5000

Api should be accessible at http://localhost:8080, while api docs are at http://localhost:8080/api/docs

Feel free to modify the .env variables as suits you best, but use .env.local. to do this.


