##  infra-homeassistant
Docker compose criado com uma infra preparada com algumas imagens para facilitar na tarefa de automação da sua residência.
HomeAssistant com suporte ao Supervisor

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
SUPERVISOR_SHARE=Dir. onde ficara sua aplicação exemplo (/opt/apl/....)
DIRETORIO_CONFIG_TIME=Dir. Volume onde ficara a configuração do time
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
```


## Como subir os containers?

1 - Entre na pasta **infra-gerenciamento-ambiente-portainer** execute o comando **docker-compose up -d** para termos o gerenciador de docker portainer

2 - Entra na pasta **infra-homeassistant** execute o comando **docker-compose up -d** para termos o gerenciador o nosso ambiente de home assistant

3 - Mova o arquivo **arquivos_configuracao/mosquitto.conf** para o **DIRETORIO_CONFIG_MOSQUITTO**

4- Acesse o portainer via http://11.5.0.2:9000, configure um usuario e senha

5 - Agora temos um home assistant e podemos configurar um mariadb, nodered e mosquisto.
