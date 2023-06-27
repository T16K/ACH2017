# ACH2017

https://github.com/T16K/wot-py
https://github.com/T16K/ACH2157

## Introdução

Este projeto demonstra a transmissão de dados do sensor UV de um microcontrolador ESP32 para um servidor Web of Things (WoT) via protocolo HTTP. O projeto utiliza a biblioteca WotPy para criação do servidor e interações com o WoT, e o microcontrolador ESP32 emparelhado com um sensor UV ML8511.

Dois principais arquivos de código compõem este projeto: server.py e main.py. O arquivo server.py configura o servidor WoT, expõe um Thing que representa o sensor UV, e define handlers customizados para leitura e gravação dos dados do sensor UV. O main.py, rodando no ESP32, periodicamente lê os dados do sensor UV e os envia para o servidor WoT usando requisições HTTP.

Este projeto serve como um exemplo base de integração de dispositivos IoT com princípios do WoT, facilitando a comunicação e a interoperabilidade entre dispositivos e aplicações dentro de um ecossistema descentralizado de IoT.

