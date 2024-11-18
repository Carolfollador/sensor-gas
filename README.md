# sensor-gas
Abstract. This paper presents the development of an IoT-based smart smoke detector, aligned with the UN Sustainable Development Goal 9 (Industry, Innovation, and Infrastructure). The system uses smoke sensors connected to a microcontroller with MQTT communication capabilities, allowing real-time monitoring and sending alerts when smoke is detected. This innovation enhances safety infrastructure by enabling early warnings in case of fire hazards, supporting resilient and sustainable urban development.

Resumo. Este artigo apresenta o desenvolvimento de um detector de fumaça inteligente baseado em IoT, alinhado ao Objetivo de Desenvolvimento Sustentável 9 (Indústria, Inovação e Infraestrutura). O sistema utiliza sensores de fumaça conectados a um microcontrolador com capacidade de comunicação via protocolo MQTT, permitindo o monitoramento remoto e o envio de alertas em tempo real em caso de detecção de fumaça. Essa inovação melhora a infraestrutura de segurança, permitindo alertas antecipados em casos de risco de incêndio, contribuindo para o desenvolvimento urbano resiliente e sustentável.

# Hardware 
Placa Arduino UNO R3
Sensor gás MQ-135
Protoboard
Sensores LED (verde e vermelho)
dois Resistor de 220Ω

# Protocolo MQTT
Embora a placa Arduino UNO R3 não tenha conexão Wi-Fi, podemos utilizar a conexão via porta USB com um script Python para estabelecer uma conexão MQTT. Isso nos permite enviar dados coletados pelo Arduino e sensor para qualquer broker escolhido. Vamos utilzar 2 cenários:
1 - Script para conexão com broker local Mosquitto

2 - Script para conexão com broker fornecido pela Adafruit.IO e criação de dashboard com dados coletados.

# Execução 
Faça as ligações pela protoboard dos dispositivos.

Conecte a uma máquina.

Será necessário python e C++ e uma IDE.

Execute o código de controle do arduino:
(```
#define sensorAnalogico A0
#define ledverde 4
#define ledvermelho 3

void setup() {
  pinMode(sensorDigital, INPUT);
  pinMode(ledverde, OUTPUT);
  pinMode(ledvermelho, OUTPUT);
  Serial.begin(9600);
  digitalWrite(ledverde, LOW);
  digitalWrite(ledvermelho, LOW);
}

void loop() {
  int ValorA = analogRead(sensorAnalogico);

  if (ValorA <= 40) {
    Serial.print("Sensor Analogico: ");
    Serial.println(ValorA);
    Serial.println("Qualidade do ar normal");
    digitalWrite(ledverde, HIGH);
    digitalWrite(ledvermelho, LOW);
  } 
  else if (ValorA > 40 && ValorA <= 75) {
    Serial.print("Sensor Analogico: ");
    Serial.println(ValorA);
    Serial.println("ATENCAO: Presença de gases nocivos no ar");
    digitalWrite(ledverde, LOW);
    digitalWrite(ledvermelho, LOW);
  } 
  else {
    Serial.print("Sensor Analogico: ");
    Serial.println(ValorA);
    Serial.println("CUIDADO: Qualidade do ar comprometida");
    digitalWrite(ledvermelho, HIGH);
    digitalWrite(ledverde, LOW);
  }

  delay(2000);
}
)
Publicando dados via MQTT:
Localmente, gerencie um broker de sua escolha e utiliza o script: local-broker.py

Para conectar com brokers externos ajuste o usuário e senha e endpoint do broker, exemplo adafruit.py
