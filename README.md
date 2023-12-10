# ACH2017-ACH2018

Este projeto demonstra a transmissão de dados de um sensor UV de um microcontrolador ESP32 para um servidor da Web of Things (WoT) via protocolo HTTP, com a funcionalidade adicional de integração de grafos RDF e um endpoint SPARQL para consultas avançadas de dados. O projeto utiliza a biblioteca WotPy para criação do servidor e interações WoT, o microcontrolador ESP32 em conjunto com um sensor UV ML8511, e RDFLib com BerkeleyDB para gerenciamento de grafos RDF.

Dois principais arquivos de código compõem este projeto: server.py e main.py. O arquivo server.py configura o servidor WoT, expõe um Thing que representa o sensor UV, e define handlers customizados para leitura e gravação dos dados do sensor UV. O main.py, rodando no ESP32, periodicamente lê os dados do sensor UV e os envia para o servidor WoT usando requisições HTTP.

Este projeto serve como um exemplo base de integração de dispositivos IoT com princípios do WoT, facilitando a comunicação e a interoperabilidade entre dispositivos e aplicações dentro de um ecossistema descentralizado de IoT.

[WoTPy](https://github.com/T16K/wot-py)

[ESP32](https://github.com/T16K/ACH2157)
