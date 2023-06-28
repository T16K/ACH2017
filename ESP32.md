# ESP32

## Descrição

Este projeto demonstra a transmissão de dados do sensor UV ML8511 de um microcontrolador ESP32 para um servidor Web of Things (WoT). O projeto utiliza a biblioteca WotPy para criação do servidor e interações com o WoT, e o microcontrolador ESP32 emparelhado com um sensor UV ML8511.

## Lista de Materiais

Antes de começar, serão necessários os seguintes componentes:
(https://github.com/T16K/ACH2157#lista-de-materiais)
- Placa de desenvolvimento ESP-WROOM-32 e cabo USB
- Sensor de Luz Ultravioleta UV ML8511
- Jumpers Macho-Macho
- Protoboard
- Fonte de Alimentação (PowerBank)

## Introdução ao ESP32

O [ESP32](https://t16k-ach2157.readthedocs.io/en/latest/comp/esp.html) é um microcontrolador amplamente utilizado para aplicações de Internet das Coisas (IoT). Com recursos avançados, como processador dual-core, conectividade Wi-Fi e Bluetooth, e diversas interfaces, o ESP32 é uma escolha popular para projetos IoT. Sua versatilidade e baixo consumo de energia tornam-no adequado para uma variedade de aplicações, desde automação residencial até dispositivos vestíveis. Nesta introdução, exploraremos os principais recursos e benefícios do ESP32.

## Introdução ao MicroPython

O [MicroPython](https://t16k-ach2157.readthedocs.io/en/latest/comp/esp.html#introduzindo-o-micropython) é uma implementação da linguagem de programação Python projetada para ser executada em microcontroladores e sistemas embarcados. Ele oferece uma abordagem simplificada e eficiente para o desenvolvimento de aplicativos para dispositivos de baixo consumo de energia e recursos limitados. Com o MicroPython, é possível escrever código Python diretamente no microcontrolador, facilitando o desenvolvimento rápido e a prototipagem de projetos.

Uma das principais vantagens do MicroPython é sua facilidade de uso e familiaridade para aqueles que já estão familiarizados com a linguagem Python. Ele permite aproveitar a ampla gama de bibliotecas e recursos disponíveis na comunidade Python, tornando mais acessível o desenvolvimento de projetos para microcontroladores.

Além disso, o MicroPython oferece recursos exclusivos, como suporte integrado para entrada e saída de pinos, gerenciamento de energia e manipulação direta de registros de hardware, permitindo um controle mais preciso do dispositivo.

Com sua combinação de simplicidade, eficiência e flexibilidade, o MicroPython tem ganhado popularidade entre desenvolvedores, makers e entusiastas de IoT que desejam aproveitar o poder da linguagem Python em dispositivos embarcados. Nesta introdução, exploraremos os recursos e benefícios do MicroPython, destacando sua versatilidade e potencial para impulsionar a criação de projetos inovadores e eficientes no mundo da eletrônica embarcada.

## Introdução ao ML8511

O [ML8511](https://t16k-ach2157.readthedocs.io/en/latest/comp/sensor.html#introduzindo-o-ml8511-uv-sensor) é um sensor de radiação ultravioleta (UV) amplamente utilizado em aplicações relacionadas à detecção e monitoramento da radiação UV. Esse sensor permite medir com precisão a intensidade dos raios UV, o que é essencial para avaliar os níveis de exposição solar e tomar medidas adequadas para proteção contra os raios UV prejudiciais. Com seu tamanho compacto e interface de comunicação simples, o ML8511 é uma escolha popular para projetos que envolvem monitoramento da radiação UV, como dispositivos de proteção solar, dispositivos vestíveis e sistemas de monitoramento ambiental. Nesta introdução, exploraremos as características e aplicações do ML8511, destacando seu papel na promoção da segurança e bem-estar em ambientes expostos à radiação UV.

## Conexões

Conectar o sensor UV ML8511 ao ESP32: 
(https://github.com/T16K/ACH2157#conex%C3%B5es)
- GND (ML8511) para GND (ESP32)
- VCC (ML8511) para 3V3 (ESP32)
- OUT (ML8511) para um pino analógico 34 (ESP32)

Escrever um código que leia os dados do sensor UV e os exiba no ESP32, usando a linguagem de programação MicroPython, que é uma versão do Python 3 otimizada para microcontroladores como o ESP32.
(https://t16k-ach2157.readthedocs.io/en/latest/software/py.html)

Para mais informações sobre o ESP32 e o Sensor ML8511, acessar o [GitHub](https://github.com/T16K/ACH2157) ou a [Documentação](https://t16k-ach2157.readthedocs.io/en/latest/)

## Servidor e Cliente

Com isso, é necessário definir como o ESP32 estará se comportando. No caso de um servidor, a instalação do WoTPy é necessária. Note que para esta configuração, não há necessidade de um gateway. Já para um cliente, um gateway se torna essencial. Este atua como intermediário entre o ESP32 e o mundo externo, facilitando a comunicação entre os dois.

Fazendo um primeiro esboço da aplicação supondo que o ESP32 seja um servidor:

Primeiro, configurar o ESP32 para ler os valores do sensor ML8511. Programando o ESP32 com um código que lê os valores do sensor a intervalos regulares. Este código será executado no ambiente de desenvolvimento MicroPython.

O ESP32 é programado para funcionar como um servidor WoT. Ele expõe a propriedade que representa o valor do sensor ML8511 através de um protocolo de rede, como HTTP.

Sempre que o ESP32 lê um valor do sensor, ele atualiza a propriedade do sensor no servidor WoT. Isso pode envolver o envio de um POST request ao servidor WoTPy ou atualizar o valor localmente se o servidor WoT estiver sendo executado no próprio ESP32.

No servidor WoTPy, criar um Thing que represente o sensor ML8511, utilizando a biblioteca WoTPy Python. O Thing deve ter uma propriedade que represente o valor atual do sensor.

Cada vez que o ESP32 enviar um novo valor do sensor para o servidor WoTPy, atualizar o valor da propriedade no Thing WoTPy que representa o sensor. Isto pode ser feito manipulando a requisição POST que o ESP32 envia e atualizando o valor da propriedade apropriadamente.

Finalmente, configurar o WoTPy para expor o Thing na rede. Isto permitirá que outros dispositivos e serviços descubram o Thing e leiam o valor do sensor.

Os clientes na rede, que também podem ser implementados usando o WoTPy ou qualquer outra biblioteca que suporte o padrão WoT, podem agora interagir com o Thing. Eles podem ler o valor atual do sensor, assinar atualizações de valor e, se suportado, acionar ações no Thing.

Mas com o decorrer da pesquisa foi descoberto que o MicroPython não suporta o WoTPy, e por isso o ESP32 será utilizado como um cliente.
