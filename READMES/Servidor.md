# Explicação do server.py

- Importando as bibliotecas e módulos necessários:
```py
import json
import logging
import tornado.gen
from tornado.ioloop import IOLoop
from wotpy.protocols.http.server import HTTPServer
from wotpy.wot.servient import Servient
```

- Definindo constantes:
```py
HTTP_PORT = 9494
ID_THING = "urn:esp32"
UV_SENSOR = "uv"
```
A constante HTTP_PORT especifica a porta na qual o servidor HTTP será executado, ID_THING é o identificador único para a "Thing" que representa o sensor UV no servidor WoT, e UV_SENSOR é o nome do recurso associado aos dados do sensor UV.

- Armazenamento global de dados:
```py
uv_data = None
```
Essa variável armazenará os dados mais recentes do sensor UV recebidos do ESP32.

- Configurando o [logging](https://docs.python.org/3/library/logging.html):
```py
logging.basicConfig()
logger = logging.getLogger()
logger.setLevel(logging.INFO)
```
Configurando o logger para exibir mensagens de log com o nível definido como INFO.

- [Descrição da Coisa](https://www.w3.org/TR/wot-thing-description/):
```py
description = {
    "id": ID_THING,
    "name": ID_THING,
    "properties": {
        UV_SENSOR: {
            "type": "number",
            "readOnly": False,
            "observable": True
        }
    }
}
```
Este dicionário representa a descrição da Coisa. Ele especifica o ID, nome e propriedades da Coisa. Nesse caso, define a propriedade UV_SENSOR como um tipo numérico que pode ser lido e observado.

- Manipuladores personalizados para leitura e gravação de dados UV:
```py
@tornado.gen.coroutine
def read_uv():
    if uv_data is None:
        return
    uv_data_dict = json.loads(uv_data.decode("utf-8"))
    return float(uv_data_dict['uv'])

@tornado.gen.coroutine
def write_uv(value):
    global uv_data
    uv_data = value
```
Essas duas funções atuam como manipuladores personalizados para a leitura e gravação dos dados do sensor UV. A função read_uv analisa os dados UV armazenados e retorna como um float. A função write_uv atualiza a variável uv_data com o valor recebido.

`tornado.gen.coroutine`: Este decorador é usado para definir uma função de coroutine no Tornado. Ele permite que a função seja usada com programação assíncrona. Você pode se referir à [documentação do Tornado](https://www.tornadoweb.org/en/stable/gen.html) para mais detalhes.

`json.loads`: Este método é usado para analisar uma string JSON em um objeto Python. Faz parte do módulo JSON do Python. Você pode se referir à [ddocumentação JSON do Python](https://docs.python.org/3/library/json.html) para mais detalhes.

uv_data.decode: Este método é usado para decodificar uma string de bytes em uma string Unicode. É um método da classe bytes em Python. Você pode se referir à [documentação de bytes do Python](https://docs.python.org/3/library/stdtypes.html#bytes.decode) para mais detalhes.

- Iniciando o servidor:
```py
@tornado.gen.coroutine
def start_server():
    http_server = HTTPServer(port=HTTP_PORT)
    servient = Servient()
    servient.add_server(http_server)
    wot = yield servient.start()
    exposed_thing = wot.produce(json.dumps(description))
    exposed_thing.set_property_read_handler(UV_SENSOR, read_uv)
    exposed_thing.set_property_write_handler(UV_SENSOR, write_uv)
    exposed_thing.expose()

if __name__ == "__main__":
    IOLoop.current().add_callback(start_server)
    IOLoop.current().start()
```

A função start_server cria um [servidor HTTP](https://agmangas.github.io/wot-py/http.html) usando a porta especificada e inicializa o [WotPy Servient](https://agmangas.github.io/wot-py/_autosummary/_wot/wotpy.wot.servient.html?highlight=servient#module-wotpy.wot.servient). Em seguida, inicia o servient, produz a Coisa com base na descrição, define os manipuladores de leitura e gravação personalizados para a propriedade UV e expõe a Coisa. Finalmente, o servidor é iniciado ao adicionar a função start_server ao IOLoop.

`servient.add_server`: Este método é usado para adicionar um servidor à instância Servient. Faz parte da biblioteca WotPy. Você pode se referir à [documentação do WotPy](https://agmangas.github.io/wot-py/_autosummary/_wot/wotpy.wot.servient.html?highlight=servient%20add_server#wotpy.wot.servient.Servient.add_server) para mais detalhes.

`servient.start`: Este método é usado para iniciar a instância Servient. Ele retorna um futuro que resolve para um objeto Wot. Faz parte da biblioteca WotPy. Você pode se referir à [documentação do WotPy](https://agmangas.github.io/wot-py/_autosummary/_wot/wotpy.wot.servient.html?highlight=servient%20start#wotpy.wot.servient.Servient.start) para mais detalhes.

`wot.produce`: Este método é usado para produzir uma instância de Coisa a partir de uma descrição de Coisa. Faz parte da biblioteca WotPy. Você pode se referir à [documentação do WotPy](https://agmangas.github.io/wot-py/_autosummary/_wot/wotpy.wot.wot.html?highlight=wot%20produce#wotpy.wot.wot.WoT.produce) para mais detalhes.

`json.dumps`: Este método é usado para serializar um objeto Python em uma string formatada em JSON. Faz parte do módulo JSON do Python. Você pode se referir à [documentação JSON do Python](https://docs.python.org/3/library/json.html) para mais detalhes.

`exposed_thing.set_property_read_handler`: Este método é usado para definir um manipulador de leitura personalizado para uma propriedade de uma Coisa. Faz parte da biblioteca WotPy. Você pode se referir à [documentação do WotPy](https://agmangas.github.io/wot-py/_autosummary/_wot/_exposed/wotpy.wot.exposed.thing.html?highlight=set_property_write_handler#wotpy.wot.exposed.thing.ExposedThing.set_property_write_handler) para mais detalhes.

`exposed_thing.set_property_write_handler`: Este método é usado para definir um manipulador de gravação personalizado para uma propriedade de uma Coisa. Faz parte da biblioteca WotPy. Você pode se referir à [documentação do WotPy](https://agmangas.github.io/wot-py/_autosummary/_wot/_exposed/wotpy.wot.exposed.thing.html?highlight=set_property_write_handler#wotpy.wot.exposed.thing.ExposedThing.set_property_read_handler) para mais detalhes.

`exposed_thing.expose`: Este método é usado para expor uma Coisa. Ele torna a Coisa disponível para interação por meio das interfaces WoT. Faz parte da biblioteca WotPy. Você pode se referir à [documentação do WotPy](https://agmangas.github.io/wot-py/_autosummary/_wot/_exposed/wotpy.wot.exposed.thing.html?highlight=expose#wotpy.wot.exposed.thing.ExposedThing.expose) para mais detalhes.
