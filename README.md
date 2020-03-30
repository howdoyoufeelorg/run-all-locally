HowDoYouFeel.org - DOCKER-COMPOSE for the entire project
=========================

This is a docker-compose script to run the entier HowDoYouFeel.org. You need to fetch the components themselves, and place them
in a directory stucture, like so:

```bash
$ mkdir admin
$ git clone  
$ mkdir api
$ git clone  
$ mkdir front
$ git clone  
```

You should then be able to run the project like so:

```bash
$ docker-compose build
$ docker-compose up -d
```

Front should be accessible at http://localhost:3000

Admin should be accessible at http://localhost:5000

Api should be accessible at http://localhost:8080, while api docs are at http://localhost:8080/api/docs

Feel free to modify the .env variables as suits you best, but use .env.local. to do this.


