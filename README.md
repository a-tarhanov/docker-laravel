## Docker for Laravel

Copy `docker` directory to project root, then

```shell
cp .env.example .env     # Init app environment
cd docker                # Go to docker directory
cp .env.example .env     # Init docker environment
make install-certs       # Install local certificate
make install-project     # Install project
```

## Make Commands

```shell
make up                  # Up containers
make stop                # Stop containers
make restart             # Restart containers
make ps                  # List containers
make logs                # Show logs
make bash                # Login to bash
make php-bash            # Login to bash php container
make www-data            # Fix rights for www-data user
make install-project     # Install project
make update-project      # Update project
make install-certs       # Install local certificate
```
