# Dependências do W3C-WoTPy

O arquivo setup.py é responsável por definir as dependências necessárias para a execução da biblioteca WotPy, conforme especificado pelo World Wide Web Consortium (W3C). Essas dependências podem ser agrupadas em duas categorias: as obrigatórias e as opcionais.

Entre as principais dependências obrigatórias definidas no arquivo setup.py, estão:

- tornado: uma biblioteca assíncrona utilizada para criar aplicativos web em Python. É empregada pela WotPy para estabelecer servidores HTTP e WebSocket.
- jsonschema: uma biblioteca que valida esquemas JSON e os dados JSON correspondentes. A WotPy utiliza essa biblioteca para validar as descrições de coisa (Thing Descriptions) recebidas e geradas.
- six: uma biblioteca que possibilita escrever código Python compatível tanto com a versão 2 quanto com a versão 3. A WotPy se beneficia dessa biblioteca para garantir a compatibilidade entre as duas versões do Python.
- rx: uma biblioteca de programação reativa que permite escrever código que responde assincronamente a mudanças de estado. É utilizada pela WotPy para suportar a API WoT Scripting e as interações com propriedades e eventos observáveis.
- python-slugify: uma biblioteca que converte strings para "slug", um formato de texto que utiliza apenas caracteres ASCII, números e traços. A WotPy utiliza essa biblioteca para criar identificadores únicos para as coisas.

Além dessas dependências obrigatórias, existem algumas dependências opcionais que a WotPy utiliza se estiverem disponíveis no sistema:

- aiocoap: uma biblioteca Python para o protocolo de transferência de dados Constrained Application Protocol (CoAP), utilizada pela WotPy para suportar o protocolo CoAP.
- hbmqtt: uma biblioteca Python para implementar o protocolo Message Queue Telemetry Transport (MQTT), utilizada pela WotPy para suportar o protocolo MQTT.
- websockets: uma biblioteca Python para suportar a comunicação via WebSocket, utilizada pela WotPy para suportar o protocolo WebSocket.
- zeroconf: uma biblioteca Python para suportar o protocolo DNS Service Discovery (DNS-SD), utilizada pela WotPy para descobrir serviços e dispositivos na rede.

Essas dependências são verificadas em tempo de execução e adicionadas ao conjunto de dependências da biblioteca WotPy, caso estejam disponíveis no sistema.
