# Sistema Gerenciador de Estoque Fibras Ópticas
Projeto de TCC que consiste no desenvolvimento de um plugin para o sistema NETBOX. O plugin fará o gerenciamento de estoque de fibras.

## Parte 1: Documentação de requisitos

A análise de requisitos aconteceu de forma progressiva, seguindo um fluxo de utilização de metodologias ágeis, como por exemplo, a utilização da dinâmica É, não é; Faz, não faz. Outras ferramentas e diagramas que foram utilizados em paralelo com as metodologias ágeis são as conversas com o interessado, Estórias de usuário, Protótipos de Tela, e Diagramas UML, sendo eles, Diagrama de Casos de Uso e Diagrama de Classes.

## Parte 2: Projeto de banco de dados

## Parte 3: Codificação da aplicação

### Configuração do ambiente:

O sistema operacional escolhido foi o Linux, com a distribuição Ubuntu. Em comparação com outros sistemas, o Ubuntu tem uma melhor performance para o desenvolvimento do plugin. As configuração de hardware para o bom funcionamento do ambiente virtual foram as seguintes:

12 GB de RAM
240 GB de armazenamento

Uma vez instalada e totalmente configurada, os próximos passos são as atualizações e instalações feitas no sistema com os seguintes comandos:

- sudo su
- apt-get update
- apt-get upgrade
- apt install aptitude -y
- aptitude install wget pluma vim -y

Obs: aptitude é um gerenciador de pacotes para a instalação nas distribuições Debian e Ubuntu.

A IDE para desenvolvimento escolhida foi o Visual Studio Code, baixado diretamente do site da Microsoft na pasta de downloads e no formato .deb. A instalação via terminal Linux é possível com o seguinte comando:

dpkg -i code_1.74.2-1671533413_amd64.deb

O desenvolvimento do plug-in para o NetBox requer o uso de containers do Docker, onde estão armazenados todo o sistema NetBox. Para tornar isso possível é necessário fazer a instalação do Docker e Docker Compose com os seguintes comandos:

- aptitude install docker docker-compose -y


Para acessar as imagens dos containers e o ambiente do NetBox é preciso baixar seu repositório github feito a partir de um clone desse repositório. O seguinte comando foi usado:

- git clone -b release https://github.com/netbox-community/netbox-docker.git

Os primeiros comandos usando o Docker são mostrados abaixo e servem para configurar o Docker para acesso às imagens dos containers e aos volumes. Foi preciso também adicionar o docker ao grupo do usuário no ubuntu, bem como mudar a permissão de acesso no arquivo docker-compose.yml por meio do editor de texto vim.

- cd netbox-docker/
- cp docker-compose.override.yml.example docker-compose.override.yml
- usermod -aG docker jose

No arquivo docker-compose.yml fez-se a alteração:
- onde estava user: 'unit:root' foi feita a troca por user: '0'

Uma outra alteraçaõ foi feita nas linhas:

- onde estava "DEBUG = _environ_get_and_map('DEBUG', 'False', _AS_BOOL)" fez-se a alteração para "DEBUG = _environ_get_and_map('DEBUG', 'True', _AS_BOOL)"
- onde estava "DEVELOPER = _environ_get_and_map('DEVELOPER', 'False', _AS_BOOL)" fez-se a alteração para "DEVELOPER = _environ_get_and_map('DEVELOPER', 'True', _AS_BOOL)"

A linha abaixo foi inserida para que tornasse possível a exibição de erros:

- TEMPLATE_DEBUG = True

Após esses procedimentos, é preciso reiniciar a máquina virtual, abrir a pasta do netbox no VS Code, abrir um novo terminal e digitar os seguintes comando que inicializam os containers:

- docker-compose pull
- docker-compose up

Após a inserção dos comandos acima, os containers serão carregados. O cotainer "netboxcommunity/netbox:v3.4-2.4.0 (c12f162eb882)" deve ser aberto por meio de um Attach Visual Code e logo em seguida abrir a pasta "/opt/netbox/netbox" (se attach não abrir esta pasta de imediato) para ter acesso ao ambiente de desenvolvimento.

## Parte 4: Testagem

## Parte 5: Implementação
