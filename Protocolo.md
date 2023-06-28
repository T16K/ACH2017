# Protocolos de Comunicação

A documentação, descreve a correspondência entre as ações de alto nível que podem ser executadas em um Dispositivo e as mensagens trocadas com o servidor ao utilizar a ligação de protocolo, por isso será feita uma brave explicação de cada protocolo.

## [Protocolo WebSockets](https://datatracker.ietf.org/doc/html/rfc6455)

O protocolo WebSockets é uma tecnologia de comunicação bidirecional baseada em TCP (Transmission Control Protocol) que permite uma conexão persistente e interativa entre um navegador web (cliente) e um servidor. Ao contrário do protocolo HTTP convencional, que é baseado em solicitação-resposta, o WebSockets permite que os dois lados estabeleçam uma conexão contínua, facilitando a transmissão de dados em tempo real.

O WebSockets é projetado para superar as limitações do HTTP em relação à comunicação em tempo real, reduzindo a sobrecarga de comunicação causada pela necessidade de abrir e fechar conexões a cada solicitação. Com o WebSockets, uma vez estabelecida a conexão inicial, tanto o cliente quanto o servidor podem enviar e receber dados em tempo real sem a necessidade de repetidas solicitações HTTP.

O protocolo WebSockets é definido pelas especificações do WebSocket, que são mantidas pelo World Wide Web Consortium (W3C) e pela Internet Engineering Task Force (IETF). O protocolo utiliza uma abordagem baseada em eventos e utiliza um handshake inicial para estabelecer a conexão entre o cliente e o servidor. Uma vez estabelecida a conexão, os dados são trocados em formato de mensagens entre as duas partes.

### Integração

O protocolo WebSockets é utilizado para executar ações de alto nível em um Thing, trocando mensagens no formato JSON-RPC 2.0 com o servidor. Os elementos de formulário associados ao WebSockets têm o formato:
```
{
"href": "ws://host.fundacionctic.org:9393/temperaturething",
"mediaType": "application/json"
}
```

As interações com o servidor WebSocket ocorrem através da troca de mensagens JSON-RPC, como mensagens de solicitação enviadas pelo cliente, mensagens de resposta enviadas pelo servidor e mensagens de erro retornadas em caso de problemas. Mensagens de Item Emitido são enviadas para inscrições ativas quando novos eventos são emitidos.

O mapeamento do modelo de interação inclui: Ler Propriedade, Escrever Propriedade, Invocar Ação, Observar Mudanças de Propriedade, Observar Evento, Observar Mudanças no TD (Thing Description) e Descartar Inscrição. Cada interação possui um formato de mensagem específico para solicitação e resposta.

## [Protocolo HTTP (Hypertext Transfer Protocol)](https://datatracker.ietf.org/doc/html/rfc7230)

O protocolo HTTP é o protocolo principal utilizado na World Wide Web para a comunicação entre clientes (navegadores) e servidores. Ele define a estrutura e as regras para solicitar e enviar recursos, como páginas da web, imagens e outros dados, por meio de uma arquitetura cliente-servidor.

O HTTP opera no topo do protocolo TCP/IP e é baseado em uma abordagem de solicitação-resposta, em que o cliente envia uma solicitação ao servidor e o servidor responde com os dados solicitados ou com um código de status que indica o resultado da solicitação. As solicitações HTTP são feitas por meio de métodos, como GET, POST, PUT e DELETE, que indicam a intenção do cliente em relação ao recurso solicitado.

O HTTP é um protocolo amplamente adotado e documentado. A especificação mais recente é a RFC 7230, que define o HTTP/1.1, amplamente utilizado na web atualmente.

### Integração

A seção descreve o mapeamento entre ações de alto nível que podem ser executadas em um Thing e as mensagens trocadas com o servidor ao usar o HTTP Protocol Binding. As mensagens são serializadas em formato JSON e os elementos de formulário variam de acordo com o tipo de interação.

O mapeamento do modelo de interação inclui: Ler Propriedade, Escrever Propriedade, Invocar Ação, Observar Mudanças de Propriedade e Observar Evento. Cada interação possui um formato específico de solicitação e resposta, e o protocolo HTTP adota o padrão de long-polling para lidar com mensagens do lado do servidor.

Ler e Escrever Propriedades envolvem requisições GET e PUT, respectivamente, e ambos retornam uma resposta HTTP 200 com o valor da propriedade. Invocar Ação envolve uma requisição POST, que inicia a invocação e retorna um UUID único. O status da invocação pode ser obtido através de uma requisição GET.

Observar Mudanças de Propriedade e Observar Evento são realizados por meio de requisições GET, e as respostas seguem o formato das ações Ler Propriedade e Observar Evento, respectivamente. As inscrições são gerenciadas automaticamente pelo HTTP Binding, sendo inicializadas em cada solicitação e canceladas após a emissão de um valor.

## [Protocolo MQTT (Message Queuing Telemetry Transport)](https://mqtt.org/getting-started/)

O protocolo MQTT é um protocolo de mensagens leve e de baixo consumo de energia projetado para comunicação de máquina para máquina (M2M) e Internet das Coisas (IoT). Ele foi desenvolvido para ser eficiente em termos de largura de banda e consumo de energia, tornando-o adequado para dispositivos com recursos limitados, como sensores e dispositivos embarcados.

O MQTT opera em um modelo de publicação/assinatura, onde os dispositivos (clientes) podem publicar mensagens em tópicos específicos, enquanto outros dispositivos podem se inscrever nesses tópicos para receber as mensagens. Isso permite uma comunicação assíncrona e distribuída, em que os dispositivos só recebem as mensagens relevantes para eles.

O protocolo MQTT é definido pela OASIS (Organization for the Advancement of Structured Information Standards) e possui várias versões, sendo a mais recente a MQTT v5.0. Ele é amplamente utilizado em cenários de IoT, onde a eficiência energética e a comunicação confiável são requisitos essenciais.

### Integração

Esta seção descreve o mapeamento entre as ações de alto nível que podem ser executadas em um Thing e as mensagens trocadas com o broker MQTT ao usar o MQTT Protocol Binding.

Diferente de outros bindings, o binding MQTT não é autossuficiente e requer a presença de um broker MQTT externo. As mensagens são serializadas em formato JSON e os elementos de formulário variam de acordo com o tipo de interação.

Os tópicos do MQTT são divididos em seis tipos diferentes usados pelos clientes e servidores para troca de mensagens. O mapeamento do modelo de interação inclui: Ler Propriedade, Observar Mudanças de Propriedade, Escrever Propriedade, Invocar Ação e Observar Evento.

Ler Propriedade envolve a publicação de uma mensagem no tópico de solicitação de propriedade, que força o servidor a publicar o valor atual da propriedade no tópico de atualização de propriedade.

Observar Mudanças de Propriedade ocorre automaticamente, com todas as mudanças de propriedade publicadas no tópico de atualização de propriedade, sem intervenção adicional do cliente.

Escrever Propriedade requer que o cliente publique uma mensagem no tópico de solicitação de propriedade, e o servidor reconhece a escrita publicando uma mensagem no tópico de confirmação de escrita de propriedade.

Invocar Ação inicia-se com a publicação de uma mensagem no tópico de invocação de ação, e o resultado da invocação é publicado no tópico de resultado de ação.

Observar Evento acontece automaticamente, com todas as emissões de evento publicadas no tópico de emissão de evento, sem intervenção adicional do cliente.

Não há necessidade de gerenciar manualmente as inscrições, pois o servidor MQTT mantém uma inscrição interna para todas as propriedades e eventos durante sua vida útil.

## [Protocolo CoAP (Constrained Application Protocol)](https://datatracker.ietf.org/doc/html/rfc7252)

O protocolo CoAP é um protocolo de aplicação web leve e projetado para dispositivos com recursos limitados, como sensores e dispositivos de IoT. Ele é semelhante ao protocolo HTTP em muitos aspectos, mas foi otimizado para operar em redes de baixa largura de banda e baixa energia, como redes sem fio de sensores.

O CoAP utiliza uma abordagem de solicitação-resposta semelhante ao HTTP, onde os clientes enviam solicitações para recursos específicos em servidores. Ele suporta métodos como GET, POST, PUT e DELETE, permitindo a leitura, gravação e exclusão de recursos.

O protocolo CoAP é definido pela RFC 7252 e é baseado no protocolo UDP (User Datagram Protocol). Ele foi projetado para ser eficiente em termos de largura de banda e consumo de energia, além de suportar a descoberta e a comunicação eficientes em redes de dispositivos de IoT.

### Integração

Esta seção descreve o mapeamento entre as ações de alto nível que podem ser executadas em um Thing e as mensagens trocadas com o servidor ao usar o CoAP Protocol Binding.

Todas as mensagens são serializadas em formato JSON. Os elementos de formulário produzidos pelo binding CoAP variam dependendo do tipo de interação. Os servidores no binding CoAP expõem três recursos distintos, um para cada tipo de interação (propriedade, ação e evento).

O mapeamento do modelo de interação inclui: Ler Propriedade, Escrever Propriedade, Observar Mudanças de Propriedade, Invocar Ação e Observar Evento. O binding CoAP aproveita o CoAP Observe para implementar mensagens do lado do servidor ao invocar ações ou assinar propriedades/eventos.

Ler Propriedade envolve o envio de uma solicitação GET para o URL CoAP correspondente. A resposta incluirá o valor da propriedade em questão.

Escrever Propriedade requer o envio de uma solicitação PUT para o URL CoAP apropriado, incluindo o novo valor da propriedade no corpo da mensagem.

Observar Mudanças de Propriedade é semelhante à ação de Ler Propriedade, exceto que o cliente deve se registrar como observador para começar a receber mensagens do lado do servidor.

Invocar Ação inicia-se com uma solicitação POST para o URL CoAP relevante, incluindo o argumento da ação no corpo da mensagem. O cliente pode verificar o status da invocação observando o recurso e passando o ID da invocação no payload.

Observar Evento envolve a criação de inscrições para o evento observando o recurso. Cada resposta do servidor para uma inscrição ativa conterá a emissão de evento mais recente.
