 __Sistema de Monitoramento e Controle com Arduino e Python:__

 
__Introdução__

Este sistema é composto por dois códigos principais, um desenvolvido para ser executado em um Arduino e outro em Python, com o objetivo de monitorar a distância medida por um sensor ultrassônico, controlar a posição de um servo motor, e registrar as leituras em um arquivo de texto no computador. O Arduino coleta dados do sensor ultrassônico e controla um servo motor baseado em um botão, enquanto o script Python recebe essas leituras do Arduino, calcula a precisão das medições e as salva em um arquivo de texto no desktop.

Este documento explica como o sistema funciona, descrevendo os principais componentes e a interação entre o código Arduino e o código Python.

__Requisitos:__

Hardware necessário:
Arduino Uno (ou qualquer outra placa Arduino compatível)
Sensor Ultrassônico (HC-SR04 ou equivalente)
Servo Motor (compatível com a biblioteca ServoTimer2)
LEDs (vermelho e verde)
Botão
Fios e Protoboard (para as conexões)
Software necessário:
Arduino IDE: Para programar o Arduino.
Python 3.x: Para executar o script Python.
Biblioteca PySerial: Para comunicação serial entre o Arduino e o script Python.
Funcionamento do Sistema

O sistema é dividido em duas partes:

__1. Código Arduino:__

O código Arduino tem como objetivo coletar as leituras do sensor ultrassônico, controlar o servo motor e acionar LEDs com base na distância medida.

Descrição do Código Arduino:
Configuração de Pins:

O triggerPin e echoPin são usados para o sensor ultrassônico.
O redLedPin e greenLedPin controlam os LEDs.
O buttonPin é utilizado para detectar a pressão de um botão.
O servoPin controla o servo motor.
Leitura da Distância: O sensor ultrassônico é utilizado para medir a distância entre o sensor e um objeto. A medição é convertida de microssegundos para centímetros.

Controle dos LEDs:

Se a distância medida for menor que 20 cm, o LED vermelho é aceso e o verde é apagado.
Se a distância for maior que 20 cm, o LED verde é aceso e o vermelho é apagado.
Controle do Servo Motor:

Quando o botão é pressionado e o LED verde está aceso, o servo motor se move para a posição correspondente a 1250 (ângulo do servo). Caso contrário, ele se mantém na posição inicial (1000).
Salvamento de Leitura: O Arduino envia as leituras de distância e o status do botão através da comunicação serial, para que o script Python as registre.

__2. Código Python:__

O código Python recebe as leituras do Arduino via comunicação serial, calcula a precisão das medições de distância e salva as informações em um arquivo de texto no desktop.

Descrição do Código Python:
Abertura de Porta Serial: O script se conecta ao Arduino através da porta serial configurada (ex.: COM5), com uma taxa de 9600 baud.

Leitura de Dados do Arduino: A cada ciclo do loop, o Python lê as mensagens enviadas pelo Arduino, que incluem a distância medida pelo sensor e o status do botão.

Cálculo da Precisão: A precisão das leituras de distância é calculada com base na proximidade do valor de 20 cm. Quanto mais distante o objeto, menor será a precisão.

Registro dos Dados: O script grava as medições em um arquivo de texto no desktop, incluindo a data, hora, distância e status do botão.

Cálculo da Média de Precisão: O script agrupa as distâncias em intervalos (com uma margem de erro de 2 cm) e calcula a média de precisão para cada grupo de distâncias
