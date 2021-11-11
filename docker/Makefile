include .env
export $(shell sed 's/=.*//' .env)

up:
	docker compose up -d $(c)

stop:
	docker compose stop $(c)

restart:
	docker compose stop $(c)
	docker compose up -d $(c)

ps:
	docker compose ps

logs:
	docker compose logs --tail=100 -f $(c)

bash:
	docker compose exec $(c) bash

php-bash:
	docker compose exec -u www-data php bash

www-data:
	docker compose exec php groupmod -o -g $(PGID) www-data
	docker compose exec php usermod -o -u $(PUID) -g www-data www-data
	docker compose exec php chown -R www-data:www-data /var/www

install-project: up www-data
	docker compose exec -u www-data php composer install
	docker compose exec -u www-data php php artisan migrate:fresh --force
	docker compose exec -u www-data php php artisan key:generate
	docker compose exec -u www-data php php artisan storage:link

update-project: up www-data
	docker compose exec -u www-data php composer install
	docker compose exec -u www-data php php artisan migrate --force

install-certs:
	mkcert localhost 127.0.0.1
	mv localhost+1.pem certs/localhost.pem
	mv localhost+1-key.pem certs/localhost-key.pem
