# ESP32

## Descrição

Este projeto tem como objetivo demonstrar o uso do microcontrolador ESP32 como cliente do servidor Web of Things (WoT), utilizando o sensor de radiação ultravioleta (UV) ML8511. Será realizado o monitoramento dos níveis de radiação UV e a transmissão desses dados para o servidor WoT. O ESP32 será configurado para se comunicar com o servidor e receber atualizações em tempo real.

## Lista de Materiais

Para o projeto, foram necessários os seguintes componentes:
(https://github.com/T16K/ACH2157#lista-de-materiais)
- Placa de desenvolvimento ESP-WROOM-32 e cabo USB
- Sensor de Luz Ultravioleta UV ML8511
- Jumpers Macho-Macho
- Protoboard
- Fonte de Alimentação (PowerBank)

## Introdução ao ESP32

O [ESP32](https://t16k-ach2157.readthedocs.io/en/latest/comp/esp.html) é um microcontrolador amplamente utilizado em aplicações de Internet das Coisas (IoT). Ele possui recursos avançados, como processador dual-core, conectividade Wi-Fi e Bluetooth, e diversas interfaces, tornando-o ideal para projetos IoT. Nesta introdução, exploraremos os principais recursos e benefícios do ESP32.

## MicroPython no ESP32

O [MicroPython](https://t16k-ach2157.readthedocs.io/en/latest/comp/ é uma implementação da linguagem de programação Python otimizada para microcontroladores e sistemas embarcados. Com o MicroPython, é possível escrever código Python diretamente no microcontrolador ESP32, facilitando o desenvolvimento e a prototipagem de projetos IoT.

## Introdução ao ML8511

O [ML8511](https://t16k-ach2157.readthedocs.io/en/latest/comp/sensor.html#introduzindo-o-ml8511-uv-sensor) é um sensor de radiação ultravioleta amplamente utilizado para detecção e monitoramento da radiação UV. Ele permite medir com precisão a intensidade dos raios UV, o que é essencial para avaliar os níveis de exposição solar e tomar medidas adequadas de proteção.

## Conexões

Conexão do sensor UV ML8511 ao ESP32: 
(https://github.com/T16K/ACH2157#conex%C3%B5es)
- GND (ML8511) para GND (ESP32)
- VCC (ML8511) para 3V3 (ESP32)
- OUT (ML8511) para um pino analógico 34 (ESP32)

Para mais informações sobre o ESP32 e o Sensor ML8511, consultar o [GitHub](https://github.com/T16K/ACH2157) ou a [Documentação](https://t16k-ach2157.readthedocs.io/en/latest/).

## Configuração como Cliente WoT

Ao realizar a pesquisa, foi constatado que o MicroPython não suporta diretamente o uso da biblioteca WoTPy. Portanto, neste projeto, o ESP32 será utilizado como cliente do servidor WoT. Isso significa que o ESP32 atuará como um dispositivo que se conecta ao servidor para receber atualizações e interagir com o WoT.

Para configurar o ESP32 como cliente WoT, é necessário estabelecer uma comunicação com o servidor WoT por meio de um gateway. O gateway funciona como intermediário, facilitando a comunicação entre o ESP32 e o servidor. Dessa forma, o ESP32 poderá enviar os dados do sensor ML8511 para o servidor e receber atualizações e comandos.

Para implementar o cliente WoT, será necessário programar o ESP32 para estabelecer a conexão com o servidor WoT e configurar a troca de dados. Isso pode ser feito por meio de requisições HTTP ou usando protocolos como MQTT ou CoAP.

Com o ESP32 configurado como cliente WoT, ele poderá receber atualizações dos dados do sensor ML8511 do servidor WoT. Esses dados podem ser utilizados para exibir informações em um display, acionar alarmes ou enviar notificações para outros dispositivos.

No contexto deste projeto, o ESP32 atuará como um cliente WoT, realizando a transmissão dos dados do sensor ML8511 para o servidor e recebendo as atualizações em tempo real.

## Tentiva de Configuração como Servidor WoT

Para confirmar a compatibilidade, foi realizada uma tentativa de instalação da biblioteca diretamente no ambiente MicroPython. Inicialmente, foi utilizado o "rshell" para transferir o arquivo "setup.py" do WoTPy para o ESP32. No entanto, verificou-se que esse arquivo não era adequado para ser carregado diretamente no ESP32.

Diante disso, buscou-se modificar a biblioteca para torná-la compatível com o MicroPython. No entanto, esse processo revelou-se complexo e demorado, envolvendo várias considerações:

- Dependências: As dependências da biblioteca precisariam ser compatíveis com o MicroPython. Muitas bibliotecas padrão do Python, como jsonschema e tornado (usadas no wotpy), não funcionam no MicroPython devido à sua complexidade e ao uso de recursos indisponíveis em microcontroladores. Seria necessário encontrar ou criar versões alternativas dessas bibliotecas que fossem compatíveis com o MicroPython.
- Recursos: As bibliotecas padrão do Python podem fazer uso de recursos e módulos que não estão disponíveis no MicroPython, como threading ou multiprocessing. Seria preciso reescrever partes da biblioteca para não depender desses recursos ou encontrar alternativas para implementar a mesma funcionalidade.
- Limitações de memória: O MicroPython é projetado para dispositivos com recursos de memória limitados. Portanto, seria necessário garantir que a biblioteca não consumisse muita memória. Isso poderia envolver a reescrita de partes da biblioteca para otimizar o uso de memória.
- Testes: Após a modificação da biblioteca, seria necessário realizar testes extensivos para garantir que ela ainda funcionasse conforme o esperado. Isso poderia ser desafiador, pois os erros podem ser menos previsíveis e mais difíceis de depurar no MicroPython em comparação com o Python padrão.

Dada a complexidade envolvida na modificação da biblioteca para torná-la compatível com o MicroPython, geralmente é mais viável buscar bibliotecas alternativas que já sejam compatíveis ou projetadas especificamente para o MicroPython.
