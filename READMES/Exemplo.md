# Exemplo de Uso

Neste projeto, foi realizado um estudo do exemplo /examples/temperature fornecido pela biblioteca WoTPy. O exemplo demonstra a criação de um servidor Web das Coisas (WoT) que simula uma entidade de temperatura com propriedades e eventos.

Inicialmente, para executar a imagem do Docker, foi utilizado o comando docker container run -ti --rm -v $PWD:/asdf 64bf8cf085ff sh. O diretório "asdf" foi escolhido arbitrariamente, enquanto "64bf8cf085ff" representa a identificação da imagem. É importante garantir que o Docker esteja em execução, utilizando o comando "systemctl start docker".

Posteriormente, foi percebido que seria mais adequado utilizar a opção --network host ao executar o contêiner. Essa opção permite que o contêiner tenha acesso direto à rede do host, facilitando a comunicação com outros dispositivos ou serviços presentes na mesma rede. O novo comando utilizado foi docker container run --network host -it --rm -v $PWD:/asdf wotpy sh.

O arquivo server.py contém a implementação do servidor WoT de temperatura. O servidor expõe uma entidade simulada de temperatura com propriedades e um evento. As propriedades incluem "temperature" (temperatura simulada) e "high-temperature-threshold" (limite superior da temperatura), ambas observáveis. O evento "high-temperature" é acionado quando a temperatura simulada ultrapassa o limite superior definido.

Para acessar as propriedades da entidade WoT, é possível fazer uma solicitação HTTP GET para a URL http://localhost:9494/properties/temperature. Isso retornará a temperatura simulada atual no formato JSON.

Para definir o limite superior da temperatura, é possível fazer uma solicitação HTTP PUT para a URL http://localhost:9494/properties/high-temperature-threshold, incluindo o valor do limite superior no corpo da solicitação em formato JSON.

Além disso, o servidor WoT de temperatura permite a comunicação bidirecional usando WebSocket. Para se conectar ao servidor WebSocket, basta abrir uma conexão WebSocket para ws://localhost:9393. Após a conexão ser estabelecida, é possível enviar mensagens para atualizar as propriedades ou receber notificações quando o evento "high-temperature" for acionado.

Essas funcionalidades do exemplo demonstram a capacidade da biblioteca WoTPy de criar servidores WoT e interagir com as entidades e eventos definidos, permitindo a integração de dispositivos e serviços na Web das Coisas de forma padronizada e interoperável.
