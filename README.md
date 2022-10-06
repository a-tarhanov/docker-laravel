## Docker for Laravel

Copy `docker` directory to project root, then

```shell
cp .env.example .env     # Init app environment
cd docker                # Go to docker directory
cp .env.example .env     # Init docker environment
make install-certs       # Install local certificate
make up                  # Up containers
```
