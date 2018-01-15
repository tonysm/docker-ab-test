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

To run the tests, you need the [Apache Benchmark](https://httpd.apache.org/docs/2.4/programs/ab.html) tool installed, run:

```bash
ab -t 10 -c 10 http://127.0.0.1:8081/
```
