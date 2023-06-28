# Protocolos de Comunicação

Esta seção apresenta uma descrição dos principais protocolos de comunicação utilizados pela biblioteca WoTPy em seus bindings. São eles: WebSockets, HTTP, MQTT e CoAP. Cada protocolo possui características e propósitos distintos, permitindo a integração eficiente de dispositivos e serviços na Web das Coisas.

## [Protocolo WebSockets](https://agmangas.github.io/wot-py/websockets.html)

O protocolo WebSockets é uma tecnologia de comunicação bidirecional baseada no TCP (Transmission Control Protocol) que permite uma conexão persistente e interativa entre um navegador web (cliente) e um servidor. Diferente do protocolo HTTP convencional, que utiliza uma abordagem de solicitação-resposta, o WebSockets permite que ambas as partes estabeleçam uma conexão contínua, facilitando a transmissão de dados em tempo real.

O WebSockets foi projetado para superar as limitações do HTTP em relação à comunicação em tempo real, reduzindo a sobrecarga de comunicação causada pela necessidade de abrir e fechar conexões a cada solicitação. Com o WebSockets, uma vez estabelecida a conexão inicial, tanto o cliente quanto o servidor podem enviar e receber dados em tempo real, sem a necessidade de repetidas solicitações HTTP.

A utilização do protocolo WebSockets na biblioteca WoTPy permite a execução de ações de alto nível em um Thing, trocando mensagens no formato JSON-RPC 2.0 com o servidor. As interações são baseadas no envio de mensagens JSON-RPC, como solicitações, respostas e notificações de eventos.

## [Protocolo HTTP (Hypertext Transfer Protocol)](https://agmangas.github.io/wot-py/http.html)

O protocolo HTTP é o principal protocolo utilizado na World Wide Web para a comunicação entre clientes (navegadores) e servidores. Ele define a estrutura e as regras para solicitar e enviar recursos, como páginas da web, imagens e outros dados, por meio de uma arquitetura cliente-servidor.

Operando sobre o protocolo TCP/IP, o HTTP é baseado em uma abordagem de solicitação-resposta, em que o cliente envia uma solicitação ao servidor e este responde com os dados solicitados ou um código de status indicando o resultado da solicitação. As solicitações HTTP são realizadas por meio de métodos, como GET, POST, PUT e DELETE, que indicam a intenção do cliente em relação ao recurso solicitado.

O protocolo HTTP é amplamente adotado e documentado, sendo a versão mais recente definida pela RFC 7230, que especifica o HTTP/1.1 amplamente utilizado na web atualmente.

Na biblioteca WoTPy, a integração com o protocolo HTTP permite a execução de ações de alto nível em um Thing, trocando mensagens serializadas em formato JSON. As interações envolvem o uso de métodos HTTP, como GET, PUT, POST e DELETE, para ler e escrever propriedades, invocar ações e observar mudanças de propriedades e eventos.

## [Protocolo MQTT (Message Queuing Telemetry Transport)](https://agmangas.github.io/wot-py/mqtt.html)

O protocolo MQTT é um protocolo de mensagens leve e de baixo consumo de energia, projetado para a comunicação de máquina para máquina (M2M) e Internet das Coisas (IoT). Ele foi desenvolvido para ser eficiente em termos de largura de banda e consumo de energia, tornando-se adequado para dispositivos com recursos limitados, como sensores e dispositivos embarcados.

Operando em um modelo de publicação/assinatura, o MQTT permite que os dispositivos publiquem mensagens em tópicos específicos, enquanto outros dispositivos se inscrevem nesses tópicos para receber as mensagens. Isso possibilita uma comunicação assíncrona e distribuída, em que os dispositivos recebem apenas as mensagens relevantes para eles.

O protocolo MQTT é definido pela OASIS (Organization for the Advancement of Structured Information Standards) e possui várias versões, sendo a mais recente a MQTT v5.0. Ele é amplamente utilizado em cenários de IoT, onde a eficiência energética e a comunicação confiável são requisitos essenciais.

A integração com o protocolo MQTT na biblioteca WoTPy permite a execução de ações de alto nível em um Thing, trocando mensagens serializadas em formato JSON com um broker MQTT externo. As interações são baseadas na publicação e assinatura de tópicos MQTT, envolvendo operações como ler propriedades, observar mudanças de propriedades, escrever propriedades, invocar ações e observar eventos.

## [Protocolo CoAP (Constrained Application Protocol)](https://agmangas.github.io/wot-py/coap.html)

O protocolo CoAP é um protocolo de aplicação web leve, projetado para dispositivos com recursos limitados, como sensores e dispositivos de IoT. Embora seja semelhante ao protocolo HTTP em muitos aspectos, ele foi otimizado para operar em redes de baixa largura de banda e baixa energia, como redes sem fio de sensores.

O CoAP utiliza uma abordagem de solicitação-resposta semelhante ao HTTP, em que os clientes enviam solicitações para recursos específicos em servidores. Ele suporta métodos como GET, POST, PUT e DELETE, permitindo a leitura, gravação e exclusão de recursos.

Definido pela RFC 7252, o protocolo CoAP é baseado no protocolo UDP (User Datagram Protocol). Ele foi projetado para ser eficiente em termos de largura de banda e consumo de energia, além de suportar a descoberta e a comunicação eficientes em redes de dispositivos de IoT.

Na biblioteca WoTPy, a integração com o protocolo CoAP permite a execução de ações de alto nível em um Thing, trocando mensagens serializadas em formato JSON. As interações envolvem o uso de métodos CoAP, como GET, PUT, POST e DELETE, para ler e escrever propriedades, observar mudanças de propriedades, invocar ações e observar eventos.
