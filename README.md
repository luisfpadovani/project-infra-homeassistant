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
  * IP verificar ao subir, configurado como host.
  * Porta *
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
PUID=10000
PGID=10000
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

1 - Entre na pasta **infra-gerenciamento-ambiente-portainer** execute o comando **docker-compose up -d** para termos o gerenciador de docker portainer

2 - Salve o arquivo **infra-homeassistant/homeassistant/mosquitto/config/mosquitto.conf** em um diretorio a parte.

3 - De a permissão de full controle na pasta **infra-homeassistant/infra-homeassistant/nodered** (Se for linux executar o comando chmod +777)

3 - Entra na pasta **infra-homeassistant** execute o comando **docker-compose up -d** para termos o gerenciador o nosso ambiente de home assistant

4 - Mova o arquivo salvos no ponto 2 para a sua origem

5- Acesse o portainer via http://11.5.0.2:9000, configure um usuario e senha e de restart nos 2 container **mosquitto** e **nodered**


