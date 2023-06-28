# Docker

## Introdução ao Docker

O Docker é uma plataforma de virtualização de contêineres que possibilita o empacotamento e distribuição de aplicativos juntamente com suas dependências. Essa tecnologia tem sido amplamente adotada no desenvolvimento de software devido aos benefícios que oferece, como a facilidade de compartilhamento de aplicativos e a garantia de reprodutibilidade do ambiente de desenvolvimento em diferentes máquinas.

## Justificativa

A escolha de utilizar o Docker neste projeto foi motivada pela necessidade de contribuir para o [repositório da biblioteca WotPy](https://github.com/agmangas/wot-py). Dado que o repositório já estava configurado para utilizar o gerenciamento de dependências em Python, optou-se por utilizar o Docker como uma solução para simplificar o processo de configuração do ambiente de desenvolvimento. Essa abordagem permite o empacotamento de todas as dependências necessárias para a biblioteca WotPy em um contêiner isolado, assegurando a consistência do ambiente de execução independentemente do sistema operacional ou das configurações locais.

Além disso, o uso do Docker traz vantagens como a portabilidade e a capacidade de isolamento. Com o Docker, torna-se possível compartilhar o ambiente de desenvolvimento completo com outros colaboradores, garantindo que todos trabalhem em um ambiente consistente. Adicionalmente, a utilização do Docker facilita a reprodução do ambiente em diferentes máquinas, evitando possíveis problemas com dependências e configurações específicas do sistema.

## Configuração do Docker

A configuração do Docker no ambiente de desenvolvimento foi realizada seguindo as instruções fornecidas na documentação oficial do Docker para instalação. O sistema operacional utilizado foi o Arch Linux, e as orientações presentes no [ArchWiki](https://wiki.archlinux.org/title/Docker#Installation) foram seguidas para garantir uma instalação adequada.

Após a instalação, verificou-se a correta configuração do Docker, assegurando que o serviço estivesse em execução e que o usuário possuísse as permissões necessárias para executar comandos do Docker.

## Criação da Imagem Docker

A criação da imagem Docker para o projeto WotPy foi realizada utilizando o [Dockerfile](https://github.com/T16K/wot-py/blob/develop/Dockerfile) disponibilizado no [repositório](https://github.com/T16K/wot-py). O Dockerfile contém as instruções necessárias para construir a imagem Docker do WotPy e suas dependências. O processo de criação da imagem foi executado utilizando o seguinte comando:
```
docker build -t wotpy .
```
Nesse comando, a opção `-t` foi utilizada para atribuir um nome à imagem, no caso, "wotpy". O Docker então executou as instruções presentes no Dockerfile, realizando a instalação das dependências necessárias e configurando o ambiente de acordo com as especificações do projeto.

## Execução do Contêiner

A execução do contêiner Docker contendo a biblioteca WotPy foi realizada utilizando o seguinte comando:
```
docker container run --network host -it --rm -v $PWD:/asdf wotpy sh
```
Nesse comando, as opções `-it` foram utilizadas para executar o contêiner em modo interativo, permitindo a interação com o terminal, e `--rm` foi usado para remover o contêiner automaticamente após a execução. O argumento fornecido foi o nome da imagem, "wotpy", para especificar qual imagem deveria ser utilizada.

A opção `--network host` foi utilizada para permitir que o contêiner tenha acesso direto à rede do host, possibilitando a utilização dos mesmos endereços IP, portas e configurações de rede. Isso facilita a comunicação entre o contêiner e outros dispositivos ou serviços presentes na mesma rede em que o host está conectado.
