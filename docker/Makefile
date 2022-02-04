include .env
export $(shell sed 's/=.*//' .env)

SHELL := /bin/bash
.PHONY: help

help:
	@echo -e "$$(grep -hE '^\S+:.*##' $(MAKEFILE_LIST) | sed -e 's/:.*##\s*/:/' -e 's/^\(.\+\):\(.*\)/\\x1b[36m\1\\x1b[m:\2/' | column -c2 -t -s :)"

up:  ## Up containers
	docker compose up -d $(c)

stop: ## Stop containers
	docker compose stop $(c)

restart: ## Restart containers
	docker compose stop $(c)
	docker compose up -d $(c)

ps: ## Show containers list
	docker compose ps

logs: ## Show containers logs
	docker compose logs --tail=100 -f $(c)

bash: ## Enter bash
	docker compose exec -u www-data php bash

install-certs: ## Install local certificates
	mkcert localhost 127.0.0.1
	mv localhost+1.pem certs/localhost.pem
	mv localhost+1-key.pem certs/localhost-key.pem
