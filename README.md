HowDoYouFeel.org - DOCKER-COMPOSE for the entire project
=========================

This is a docker-compose script to run the entier HowDoYouFeel.org. You need to fetch the components themselves, and place them
in a directory stucture, like so:

```bash
$ git clone git@github.com:howdoyoufeelorg/api.git  
$ git clone git@github.com:howdoyoufeelorg/admin.git
$ git clone git@github.com:howdoyoufeelorg/front.git
```

You should then be able to run the project like so:

```bash
$ docker-compose build
$ docker-compose up -d
```

The first thing to do is to install composer dependencies:

```bash
$ docker-compose exec api composer install
```

The proces should also create the SSH keys for JWT token. You should see the SSH keys in api/config/jwt. 
If they're not created, there's a procedure here  

https://github.com/lexik/LexikJWTAuthenticationBundle/blob/master/Resources/doc/index.md#generate-the-ssh-keys

Then you need to create the tables in the database. You do this via api container doctrine commands, like so:

```bash
$ docker-compose exec api bin/console doctrine:schema:create 
```

Finally, you can activate fixtures to create a test user and an initial set of questions:
 
```bash
$ docker-compose exec api bin/console doctrine:fixtures:load -q
```

Test user credentials are:
```
email: test@howdoyoufeel.org
password: TestHowDoYouFeel
```
Front should be accessible at http://localhost:3000

Admin should be accessible at http://localhost:5000

Api should be accessible at http://localhost:8080, while api docs are at http://localhost:8080/api/docs

Feel free to modify the .env variables as suits you best, but use .env.local to do this.


