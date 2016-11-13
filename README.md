## How to use

This system requires "phinx" as database migration tool, [Please install "composer"](http://qiita.com/CatCable/items/02364adacf36410f449e)

```bash
# clone this
git clone {this repository}
cd {cloned directory}
 
# If you have not start VM yet, you should start it.
docker-machine start {VM name}
eval "$(docker-machine env default)"
 
# run docker containers
cp docker-compose.example.yml docker-compose.yml
docker-compose build
docker-compose up -d
 
# migrate database
cd migration
composer install
./vendor/bin/phinx init 
/bin/cp -f migration/phinx.example.yml migration/phinx.yml
./vendor/bin/phinx migrate -e development
 
# test request by curl
curl -i http://`docker-machine ip | tr -d '\n'`
 
# login mysql as root
mysql -h `docker-machine ip | tr -d '\n'` -uroot -ppass
```
