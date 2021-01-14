# Docker + PHP 8.0 + Lumen 8 + MySQL 8.0 + NGINX

---
### Requisitos
- Docker

### Instalação
Para executar o container, execute:
```sh
$ docker-compose up lumen
```
Para executar o container em background, execute com o parâmetro "-d": `docker-compose up -d lumen`

Execute o comando `composer update` para criar/atualizar a pasta vendor, é necessário que o container esteja rodando, execute:
```sh
docker exec -it lumen composer update
```

#### Migrates
Para rodar as migrates, execute:
```sh
docker exec -it lumen php artisan migrate --seed
```
