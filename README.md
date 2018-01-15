# This repository is for testing only.

Not a Laravel test, but a docker one.

## Setting up

Run:

```bash
cp .env.example .env
composer install
php artisan key:generate

docker-compose up -d

sudo chown -R $(id -u):www-data ./
sudo chmod -R ug+rw .
```

### Registering the testing vhost locally

Since we are using vhosts now, we need to register some entries in our `/etc/hosts` file. Make sure you have these there: `127.0.0.1 mwl.localhost php.localhost`. You can remove it after you finish the tests.

To run the tests, you need the [Apache Benchmark](https://httpd.apache.org/docs/2.4/programs/ab.html) tool installed, run:

```bash
ab -t 10 -c 10 http://mwl.localhost/
```

and

```bash
ab -t 10 -c 10 http://php.localhost/
```

If you want to, you can boot only the PHP or the MWL versions of the containers and perform the ab test on those. You can do so by running `docker-compose up -d php` or `docker-compose up -d mwl`. This way, you will have to run the tests against the `http://127.0.0.1:{APP_PORT}` where `APP_PORT` is the one defined in the `docker-compose.yml` file.
