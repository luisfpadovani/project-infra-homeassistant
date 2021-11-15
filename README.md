# infra-homeassistant
Docker compose criado com uma infra preparada com algumas imagens para facilitar na tarefa de automação da sua residência.

## _Imagens utilizdas_
- HomeAssistant (Sistema de controle central para dispositivos domésticos inteligentes)
- NodeRed (Para criação de workflows)
- Mosquitto (MQTT)
- Mariadb (Banco de dados)
- Portainer (Gerenciador do Docker)

## Containers Criados

* Home Assistant
  * IP 10.5.0.2 
  * Porta 443/8123
* NodeRed
  * IP 10.5.0.4 
  * Porta 1880
* Mosquisto
  * IP 10.5.0.5  
  * Porta 1883/1884
* MariaDB
  * IP 10.5.0.3 
  * Porta 3306
* Portainer
  * IP 11.5.0.2
  * Porta 9000

## Instalação

Para a instação é necessário criar dois arquivos:

**.env** com as seguintes configurações

```sh
COMPOSE_FILE=infra-gerenciamento-ambiente/gerenciador-docker.yaml:infra-homeassistant/home-assistant.yaml
MYSQL_ROOT_PASSWORD=<suasenha1aqui>
HA_MYSQL_PASSWORD=<suasenha2aqui>
PUID=0
PGID=0
```

**configuration.yaml** no diretorio **home-assistant-config**
```
default_config:
panel_iframe:
  nodered:
    title: Node-Red
    icon: mdi:shuffle-variant
    url: http://10.5.0.4:1880/
    require_admin: true
mqtt:
  broker: 10.5.0.5
  
recorder:
  db_url: mysql://homeassistant:<suasenha2aqui>@10.5.0.3/ha_db?charset=utf8
  purge_keep_days: 30
```

## Como subir os containers?

Na raiz do projeto execute **docker-compose up**