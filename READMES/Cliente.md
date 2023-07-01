# Cliente Web of Thing (WoT)

O código [main.py](https://github.com/T16K/wot-py/blob/develop/examples/uv_sensor/main.py) implementa um cliente Web of Things (WoT) no dispositivo ESP32, permitindo a interação com sensores e o envio dos dados para um servidor WoT. O cliente WoT é responsável por buscar informações dos sensores e controlar as funcionalidades dos dispositivos conectados de maneira padronizada e interoperável.

O cliente WoT utiliza o protocolo HTTP para se comunicar com o servidor WoT. No código, é feito uso da biblioteca urequests para realizar solicitações HTTP PUT ao servidor. Essas solicitações enviam os dados dos sensores em formato JSON para o servidor WoT, permitindo que os dados sejam armazenados e acessados pelos usuários.

O código define os sensores utilizados no dispositivo ESP32, como o sensor de UV, e suas configurações. Cada sensor possui uma identificação única e é associado a uma descrição no formato de Thing Description (TD). A TD contém informações sobre o sensor, como os links de acesso aos dados no servidor WoT.

A função send_sensor_data é responsável por enviar os dados dos sensores para o servidor WoT. Ela recebe como parâmetros a identificação do sensor, o tipo de sensor, o URL de acesso aos dados na TD e os dados a serem enviados. A função realiza uma solicitação HTTP PUT ao URL especificado, enviando os dados em formato JSON. Se a solicitação for bem-sucedida, uma mensagem de sucesso é exibida. Caso contrário, uma mensagem de falha é exibida juntamente com o código de status da resposta.

No loop principal main(), os valores dos sensores são lidos periodicamente. A cada iteração do loop, os dados dos sensores são obtidos e enviados para o servidor WoT utilizando a função send_sensor_data. Esse processo permite que os dados dos sensores sejam atualizados no servidor WoT em tempo real, possibilitando que os usuários acessem e utilizem essas informações de forma padronizada.

Em resumo, o código implementa um cliente WoT no ESP32, permitindo a comunicação com sensores e o envio dos dados para um servidor WoT por meio do protocolo HTTP. O uso da Thing Description (TD) possibilita a descrição dos dispositivos e a padronização das interações com o servidor. Essa abordagem permite que os usuários acessem os dados dos sensores de forma fácil e interoperável, promovendo a criação de aplicações e serviços baseados na Web of Things.
