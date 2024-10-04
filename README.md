# CP5 - Edge Computing

## Integrantes 👋
<ul>
    <li>Gabriel Barros (RM556309)</li>  
    <li>João Marcelo Furtado Romero (RM555199)</li>
    <li>Kayky Silva Stiliano (RM555148)</li>
    <li>Pedro Henrique Bizzo de Santana (RM557263)</li>
    <li>Pedro Henrique Mendes (RM555332)</li>
</ul>
 
<img src="./screenshot ESP32.png" alt="print do circuito Arduino/printscreen Arduino circuit"/>

Link da simulação no <a href="[path](https://wokwi.com/projects/410377764841984001)">Wokwi</a>

## Instruções
Para fazer o projeto funcionar primeiro inicie o Wokwi e depois inicie o programa python.

## Explicação do Projeto 📖
Este projeto consiste em dois componentes principais:
<ul>
    <li>fiware_IOT.cc: Código para um dispositivo IoT baseado em ESP32 que lê dados de sensores (como DHT e luminosidade), conecta-se a uma rede Wi-Fi e publica/recebe informações de um Broker MQTT.</li>
    <li>web_paho.py: Um servidor web em Flask que exibe os dados do dispositivo IoT em gráficos em tempo real, utilizando WebSockets para comunicação em tempo real e Paho MQTT para receber dados do dispositivo.</li>
</ul>
 
## Componentes 🛠️
<ul>
    <li>ESP32</li>
    <li>DHT11/22</li>
    <li>LDR</li>
    <li>LED</li>
    <li>Potenciomêtros</li>
</ul>
 
<br>

## Explicando o <a href="./fiware_IOT.cc">Código</a> 🧑‍💻

### Dependências 📦
<ul>
    <li>WiFi.h</li>
    <li>PubSubClient.h</li>
    <li>DHT.h</li>
</ul>
 
<br>
 
### `fiware_IOT.cc`
Este código é responsável por conectar o dispositivo IoT à rede Wi-Fi e ao Broker MQTT para enviar e receber dados dos sensores e controlar o estado de saída do dispositivo (como o LED onboard).

**Principais Funcionalidades**:
<ul>
    <li>Wi-Fi: Conexão com a rede Wi-Fi utilizando o nome e senha configurados.</li>
    <li>MQTT: Publicação e assinatura em tópicos MQTT para enviar dados de sensores e receber comandos do broker.</li>
    <li>Tópicos utilizados:</li>
        <ul>
            <li>/TEF/device010/attrs: Publica o estado do dispositivo.</li>
            <li>/TEF/device010/attrs/p: Publica o valor da luminosidade (potenciômetro).</li>
            <li>/TEF/device010/attrs/dht: Publica dados do sensor DHT (temperatura e umidade).</li>
            <li>/TEF/device010/cmd: Recebe comandos para controlar o dispositivo (ex: ligar/desligar LED).</li>
        </ul>
    <li>DHT22: Leitura de temperatura e umidade usando o sensor DHT22.</li>
    <li>Luminosidade: Lê valores de luminosidade simulados e os publica no Broker MQTT.</li>
    <li>Callback MQTT: Executa ações com base em mensagens recebidas, como ligar/desligar o LED onboard.</li>
    <li>Gerenciamento de Conexões: Reconecta automaticamente ao Wi-Fi e ao Broker MQTT em caso de desconexão.</li>
</ul>

<br>

## Explicando o <a href="./web_paho.py">Código</a> 🧑‍💻

### Dependências 📦
<ul>
    <li>Flask</li>
    <li>Flask-SocketIO</li>
    <li>Paho-MQTT</li>
    <li>Chart.js</li>
    <li>Bootstrap</li>
</ul>
 
<br>

### `web_paho.py`
Este código implementa um servidor web que utiliza Flask para servir uma página HTML que exibe os dados recebidos do dispositivo IoT em tempo real.

**Principais Funcionalidades**:
<ul>
    <li>MQTT: Assina os tópicos /TEF/device010/attrs/p (potenciômetro) e /TEF/device010/attrs/dht (DHT) e atualiza a página web com os dados recebidos.</li>
    <li>WebSocket: Utiliza SocketIO para enviar os dados recebidos via MQTT para a interface do usuário em tempo real.</li>
    <li>Gráficos em Tempo Real: Utiliza o Chart.js para exibir gráficos de "gauge" (medidores) para a velocidade (potenciômetro), temperatura e umidade.</li>
    <li>Página Web: Interface web com Bootstrap para layout e gráficos para visualização dos dados.</li>
</ul>

## Como Usar

### 1. Dispositivo IoT (`fiware_IOT.cc`)
<ul>
    <li>Carregue o código `fiware_IOT.cc` em um ESP32.</li>
    <li>Certifique-se de configurar as credenciais Wi-Fi e o endereço IP do Broker MQTT.</li>
    <li>O dispositivo começará a publicar os dados dos sensores DHT e luminosidade para os tópicos configurados, além de receber comandos para ligar/desligar o LED.</li>
</ul>

### 2. Servidor Web (`web_paho.py`)
<ul>
    <li>Instale as dependências do Python: Flask, Flask-SocketIO, Paho-MQTT. </li>
    <li>Execute o arquivo web_paho.py para iniciar o servidor web.</li>
    <li>Acesse http://localhost:5000 em seu navegador para visualizar os dados em tempo real.</li>
</ul>

## Estrutura de Tópicos MQTT

| Tópico                        | Descrição                                     |
|-------------------------------|-----------------------------------------------|
| `/TEF/device010/attrs`         | Publicação do estado do LED (ligado/desligado)|
| `/TEF/device010/attrs/p`       | Publicação do valor do potenciômetro          |
| `/TEF/device010/attrs/dht`     | Publicação de temperatura e umidade           |
| `/TEF/device010/cmd`           | Assinatura de comandos para controle do LED   |

<br>












<center>Este projeto encontra sob a <a href="https://github.com/Formula-E-Mahindra-Racing/Sprint1-Edge/blob/main/LICENSE">MIT License.</a></center>
