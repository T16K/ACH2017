# Servidor Web of Things (WoT)

O servidor Web of Things (WoT) é uma peça fundamental na arquitetura WoT, pois é responsável por expor os dispositivos conectados e suas funcionalidades para que possam ser descobertos e interagidos pelos clientes. O servidor WoT atua como uma ponte entre os dispositivos da Internet das Coisas (IoT) e os aplicativos e serviços que desejam acessá-los.

O código [server.py](https://github.com/T16K/wot-py/blob/develop/examples/uv_sensor/server.py) implementa um servidor Web of Things (WoT) que expõe uma Thing (dispositivo) responsável por fornecer os valores de um sensor de UV. O servidor WoT permite a descoberta e interação com a Thing por meio de solicitações HTTP padronizadas.

O servidor WoT utiliza a biblioteca Tornado e o protocolo HTTP para receber solicitações dos clientes e responder de acordo com as interações definidas na descrição da Thing. A Thing é definida por uma descrição no formato de um documento JSON, que especifica suas propriedades e comportamentos.

No código, é criado um HTTP server na porta especificada (HTTP_PORT) e um Servient, que é uma instância responsável por gerenciar os recursos WoT. A descrição da Thing é definida, contendo o identificador (ID_THING) e as propriedades, como o sensor de UV.

Para cada propriedade da Thing, como o sensor de UV, são definidos os manipuladores de leitura (read_uv) e escrita (write_uv). O manipulador de leitura é responsável por retornar o valor atual do sensor quando solicitado pelo cliente. O manipulador de escrita é responsável por atualizar o valor do sensor quando recebido uma solicitação de escrita do cliente.

Ao iniciar o servidor, é criado o objeto WoT, e a Thing é produzida com base na descrição. Em seguida, os manipuladores de leitura e escrita são associados à propriedade correspondente na Thing. Isso permite que o servidor WoT responda às solicitações de leitura e escrita para o sensor de UV.

Por fim, a Thing é exposta e o servidor inicia seu loop de eventos, aguardando as solicitações dos clientes e respondendo de acordo com as interações definidas.

Em resumo, o código implementa um servidor WoT que expõe uma Thing representando um sensor de UV. O servidor utiliza o protocolo HTTP e a biblioteca Tornado para receber e responder solicitações dos clientes. A descrição da Thing é definida, e manipuladores de leitura e escrita são associados às propriedades da Thing. Isso permite que os clientes leiam e escrevam dados no servidor WoT de forma padronizada e interoperável.
