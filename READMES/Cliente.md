# Explicação do main.py

- Importando os módulos necessários:
```py
import machine
import ujson
import urequests
import time
```

- Configuração do sensor:
```py
sensors = {
    'uv_sensor': {'type': 'uv', 'sensor': machine.ADC(machine.Pin(34))},
    # Add sensors as needed
}
```

Este dicionário contém as configurações do sensor. Neste caso, ele define um uv_sensor com seu tipo como 'uv' e especifica o pino correspondente no ESP32.

`machine.ADC`: Esta classe faz parte do módulo machine do MicroPython e é usada para configurar e ler valores de um canal do Conversor Analógico-Digital (ADC). Você pode se referir à documentação do MicroPython machine.ADC para mais detalhes.

`machine.Pin`: Esta classe faz parte do módulo machine do MicroPython e é usada para configurar e controlar os pinos GPIO. Você pode se referir à documentação do MicroPython machine.Pin para mais detalhes.

- Descrição da Coisa:
```py
TD = {
    'uv_sensor': {"links": [{"href": "http://000.000.0.00:9494/urn:esp32/property/uv"}]},
}
```

O dicionário TD contém as descrições das Coisas. Ele contém um link para a propriedade do sensor UV no servidor.

Função para enviar dados do sensor para o servidor:
```py
def send_sensor_data(sensor_id, sensor_type, url, data):
    headers = {'content-type': 'application/json'}
    try:
        r = urequests.put(url.format(sensor_id), data=ujson.dumps(data), headers=headers)
        if r.status_code >= 200 and r.status_code < 300:
            print('Successfully sent {} data from {} to WoT server'.format(sensor_type, sensor_id))
        else:
            print('Failed to send {} data from {} to WoT server: received status code {}'.format(sensor_type, sensor_id, r.status_code))
        r.close()
    except Exception as e:
        print('Could not send {} data from {} to WoT server: '.format(sensor_type, sensor_id), e)
```

Esta função recebe o ID do sensor, tipo, URL e dados como entrada. Ela envia uma solicitação HTTP PUT para o servidor com a carga de dados no formato JSON. Em seguida, imprime uma mensagem de sucesso ou falha com base no código de status da resposta.

`ujson.dumps`: Esta função é fornecida pelo módulo ujson do MicroPython e é usada para serializar um objeto Python em uma string formatada em JSON. Você pode se referir à [documentação do MicroPython ujson](https://docs.micropython.org/en/latest/library/json.html) para mais detalhes.

`urequests.put`: Esta função é fornecida pelo módulo urequests do MicroPython e é usada para enviar uma solicitação HTTP PUT. É similar à biblioteca requests em Python. Você pode se referir à [documentação do MicroPython urequests](https://makeblock-micropython-api.readthedocs.io/en/latest/public_library/Third-party-libraries/urequests.html) para mais detalhes.

- Função principal:
```py
def main():
    while True:
        for sensor_id, sensor_info in sensors.items():
            sensor_value = sensor_info['sensor'].read()
            data = {sensor_info['type']: sensor_value}
            url = TD[sensor_id]['links'][0]['href']
            send_sensor_data(sensor_id, sensor_info['type'], url, data)
        time.sleep(5)

if __name__ == "__main__":
    main()
```

A função principal é executada quando o script é executado. Ela entra em um loop infinito e itera através de cada sensor definido no dicionário sensors. Lê o valor do sensor, cria um objeto de dados com o tipo correspondente, recupera a URL da Descrição da Coisa (TD) e chama a função send_sensor_data para enviar os dados para o servidor. O loop aguarda 5 segundos antes de repetir.

`time.sleep`: Esta função faz parte do módulo time do Python e é usada para pausar a execução do programa por um número especificado de segundos. Você pode se referir à [documentação do Python time](https://docs.python.org/3/library/time.html#time.sleep) para mais detalhes.

# Explicação do boot.py

O arquivo boot.py é um script que é executado automaticamente quando o ESP32 é iniciado. Seu objetivo é estabelecer uma conexão Wi-Fi com a rede especificada, permitindo que o ESP32 se conecte à internet e se comunique com o servidor WoT.

O código define uma função chamada `do_connect` que recebe o SSID (nome da rede) e a senha como argumentos. Dentro da função, ele importa o módulo de rede para gerenciar a conexão Wi-Fi.

A função verifica se o ESP32 já está conectado a uma rede usando o método `isconnected` da interface `STA_IF` (interface de estação). Se o ESP32 não estiver conectado, ele procede para se conectar ativando a interface de estação `(active(True))` e chamando o método connect com o SSID e a senha fornecidos.

Após iniciar a conexão, o código entra em um loop que espera até que o ESP32 se conecte com sucesso à rede (`isconnected()` retorna `True`).

Uma vez que a conexão é estabelecida, ele imprime os detalhes de configuração da rede (endereço IP, máscara de sub-rede, gateway, etc.) usando o método ifconfig da interface de estação.

Para usar este script, substitua 'YourSSID' pelo SSID da sua rede Wi-Fi e 'YourPassword' pela senha correspondente.

Ao incluir este script boot.py no seu ESP32, ele se conectará automaticamente à rede Wi-Fi especificada na inicialização, garantindo uma conexão à internet confiável para sua aplicação.

Lembre-se de fazer upload do arquivo boot.py modificado para o ESP32 e verificar se as credenciais da rede estão corretas antes de implantar seu projeto.
