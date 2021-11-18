# infra-homeassistant
Docker compose criado com uma infra preparada com algumas imagens para facilitar na tarefa de automação da sua residência.

## _Imagens utilizdas_
- HomeAssistant (Sistema de controle central para dispositivos domésticos inteligentes)
- ghcr.io/linuxserver/swag (Proxy reverso)
- NodeRed (Para criação de workflows)
- Mosquitto (MQTT)
- Mariadb (Banco de dados)
- Portainer (Gerenciador do Docker)

## Containers Criados

* Swag
  * IP verificar ao subir,.
  * Porta 8080/443
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

DIRETORIO_CONFIG_HOMEASSISTANT=Dir. Volume onde ficara a configuração do home assistant
DIRETORIO_CONFIG_TIME=Dir. Volume onde ficara a configuração do time
DIRETORIO_CONFIG_SWAG=Dir. Volume onde ficara a configuração da swap (proxy reverso)
DIRETORIO_CONFIG_MARIADB=Dir. Volume onde ficara a configuração do banco de dados
DIRETORIO_CONFIG_MOSQUITTO=Dir. Volume onde ficara a configuração do mosquitto
DIRETORIO_LOG_MOSQUITTO=Dir. Volume onde ficara os logs do mosquitto
DIRETORIO_DATA_MOSQUITTO=Dir. Volume onde ficara todos os dados do mosquitto
DIRETORIO_DATA_NODERED=Dir. Volume onde ficara todos os dados do mosquitto


MYSQL_ROOT_PASSWORD=<suasenha1aqui>
HA_MYSQL_PASSWORD=<suasenha2aqui>
PUID= (id do usuario que ira criar as pastas)
PGID=  (id do usuario que ira criar as pastas)
ZONA_PAIS=America/Sao_Paulo
URL_DUCKDNS= DNS CRIADO NO DUCK DNS PARA EXPOR PARA EXTERNO
TOKEN_DUCKDNS= TOKEN QUE FOI CRIADO NA SUA CONTA DO DUCK DNS
EMAIL_SWAG=SEU EMAIL
```

**configuration.yaml** no diretorio **home-assistant-config**
```
# Configure a default setup of Home Assistant (frontend, api, etc)
default_config:
#Monitora o ambiente
system_health:
# Text to speech
tts:
  - platform: google_translate
#CONFIGURACAO REDE
http:
  server_port: 8123
  server_host: # Server Host
  ip_ban_enabled: true
  login_attempts_threshold: 3
  use_x_forwarded_for: true
  trusted_proxies:
    -  # Local Lan
    -  # Docker network
    -  # Proxy
duckdns:
  domain: dominioduckdns
  access_token: tokendns
homeassistant:
  internal_url: "http://<iphost>:8123"
  external_url: "https://dominioduckdns.duckdns.org"  

#PAINEL LATERAL
panel_iframe:
#NODERED
  nodered:
    title: Node-Red
    icon: mdi:shuffle-variant
    url: http://10.5.0.4:1880/
    require_admin: true
#MQTT
mqtt:
  broker: 10.5.0.5    
#BANCO DE DADDOS 
recorder:
  db_url: mysql://homeassistant:<suasenha2aqui>@10.5.0.3/ha_db?charset=utf8
  purge_keep_days: 30

#INCLUDES
group: !include groups.yaml
automation: !include automations.yaml
script: !include scripts.yaml
scene: !include scenes.yaml  
```


## Como subir os containers?

1 - Entre na pasta **infra-gerenciamento-ambiente-portainer** execute o comando **docker-compose up -d** para termos o gerenciador de docker portainer

2 - Entra na pasta **infra-homeassistant** execute o comando **docker-compose up -d** para termos o gerenciador o nosso ambiente de home assistant

3 - Mova o arquivo **arquivos_configuracao/mosquitto.conf** para o **DIRETORIO_CONFIG_MOSQUITTO**

4 - Mova o arquivo **configuration.yaml** criado  para **DIRETORIO_CONFIG_HOMEASSISTANT**

5 - Configure o proxy reverso de acordo com o nome do SUBDOMINIO que você deu para o home assistant. (para mais informações podem acessar a imagem) [https://github.com/linuxserver/docker-swag]

6- Acesse o portainer via http://11.5.0.2:9000, configure um usuario e senha e de restart nos 3 container **mosquitto**, **nodered** e **homeassistant**


