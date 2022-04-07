##  infra-homeassistant
Docker compose criado com uma infra preparada para facilitar na tarefa de automação da sua residência.
Importante ressaltar que o docker-compose não oferece a IMAGEM do Home Assistant, é de total responsabilidade o usuario instalar o Home Assistant.

**Abaixo coloco o link da infra do home assistant que estou utilizando, ela oferece suporte ao supervisor, para instala-la é necessário seguir alguns requisitos.**
#### Pre-requisitos
1. Ter os requisitos de softwares atendidos que estão apontados em **3.a**
1. Inserir o dentro do arquivo **etc/hosts** o host/ip **140.82.121.34 ghcr.io**
 * Bug que existe ao tentar instalar o agente supervised.
1. Instalar o Home Assistant Supervised
 * Seguindo o tutorial de instalação https://github.com/home-assistant/supervised-installer de acordo com a arquitetura do seu hardware.


## _Imagens utilizdas_
- Portainer (Gerenciador do Docker)

## Containers Criados
* Home Assistant
  * IP verificar ao subir, configurado como host.
  * Porta 8123
* Portainer
  * IP 11.5.0.2
  * Porta 9000

## Como subir os containers?

1 - Entre na pasta **infra-gerenciamento-ambiente-portainer** execute o comando **docker-compose up -d** para termos o gerenciador de docker portainer

2 - Acesse o portainer via http://11.5.0.2:9000, configure um usuario e senha

3 - Agora temos um home assistant e podemos configurar um mariadb, nodered e mosquisto.
