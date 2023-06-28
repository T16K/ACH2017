# Exemplo de Uso

Para ter uma melhor compreensão da biblioteca WoTPy, estudei o exemplo `/examples/temperature`, para isso utilizei o comando docker para executar a imagem. O diretório "asdf" foi escolhido arbitrariamente, enquanto "64bf8cf085ff" representa a identificação da imagem. É importante lembrar de garantir que o Docker esteja em execução, utilizando o comando "systemctl start docker".
```
docker container run -ti --rm -v $PWD:/asdf 64bf8cf085ff sh

```

Mais tarde, foi percebido que seria melhor utilizar a opção `--network host` para permitir que o contêiner tenha acesso direto à rede do host, possibilitando a utilização dos mesmos endereços IP, portas e configurações de rede. Isso facilita a comunicação entre o contêiner e outros dispositivos ou serviços presentes na mesma rede em que o host está conectado.
```
docker container run --network host -it --rm -v $PWD:/asdf wotpy sh
```

Arquivo server.py (Simulação de Temperatura)

Este é um servidor Web das Coisas (WoT) que expõe uma entidade simulada de temperatura com duas propriedades e um evento.

O servidor WoT de temperatura expõe uma entidade com as seguintes propriedades e evento:

- Propriedade temperature: um número de ponto flutuante que representa a temperatura simulada, com somente leitura e observável.
- Propriedade high-temperature-threshold: um número de ponto flutuante que representa o limite superior da temperatura, observável e pode ser alterado.
- Evento high-temperature: acionado quando a temperatura simulada ultrapassa o limite superior definido.
Para acessar a entidade WoT e suas propriedades, você pode fazer uma solicitação HTTP GET para a seguinte URL: (http://localhost:9494/properties/temperature). Isso retornará a temperatura simulada atual em formato JSON.

Para definir o limite superior da temperatura, você pode fazer uma solicitação HTTP PUT para a seguinte URL: (http://localhost:9494/properties/high-temperature-threshold). Inclua o valor do limite superior no corpo da solicitação em formato JSON.

O servidor WoT de temperatura também permite a comunicação bidirecional usando WebSocket. Para se conectar ao servidor WebSocket, abra uma conexão WebSocket para (ws://localhost:9393).

Uma vez conectado, você pode enviar mensagens para atualizar as propriedades ou receber notificações quando o evento "high-temperature" é acionado. 

