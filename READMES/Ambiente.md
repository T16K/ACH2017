# Configuração do Ambiente

## Servidor WoT

Este documento pressupõe que você tenha o docker instalado na sua máquina. Caso contrário, visite o [site oficial](https://docs.docker.com/get-docker/) para instalá-lo.

Primeiro, execute os seguintes comandos no seu terminal:
```sh
git clone https://github.com/T16K/wot-py.git
cd wot-py
docker build .
```

Agora você construiu uma imagem a partir do Dockerfile. Em seguida, verifique o IMAGE ID:
```sh
docker images
```

Copie os caracteres na coluna IMAGE ID e substitua 'IMAGE_ID' no seguinte comando:
```sh
docker container run --network host -it --rm -v $PWD:/asdf 'IMAGE_ID' sh
```

Agora estamos executando um container Docker usando a imagem especificada com a pilha de rede do host, que fornece acesso interativo a uma sessão de shell, e montando o diretório de trabalho atual no diretório /asdf dentro do container.

Finalmente, acesse o arquivo server.py, e temos o servidor em execução:
```sh
cd examples/uv_sensor
python server.py
```

## ESP32

Para informações detalhadas, consulte este [documento](https://t16k-ach2157.readthedocs.io/en/latest/comp/esp.html).
