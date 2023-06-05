README 
- EDGE COMPUTING & COMPUTER SYSTEMS 

Links de acesso: 

YouTube -> https://youtu.be/eiK_wp_ptEc
GitHub ->
TinkerCad -> https://www.tinkercad.com/things/g0jwMeo7Ttl


Membros do grupo: 

Guilherme Catelli Bichaco - 97989
Vinicius Sobreira Borges - 97767
Lucas Almeida de Siqueira - 551854
Lucas Laia Manentti - 97709
Enzo de Oliveira Cunha - 550985


------- 

# Controle de Temperatura e Umidade para Transporte de Alimentos

Este é um projeto que utiliza o Arduino para controlar a temperatura e umidade durante o transporte de alimentos. O sistema é alimentado por um banco de dados que contém informações sobre diferentes alimentos, suas propriedades nutricionais e combinações possíveis. Com base nesses dados, uma IA generativa cria receitas personalizadas que atendem aos requisitos nutricionais de cada indivíduo. O foco principal do problema é garantir o transporte e armazenamento seguro dos alimentos até a doação e consumo.

## Solução Proposta

A solução proposta consiste em utilizar um projeto interativo com veículos de transporte e armazéns. Um sensor de temperatura e um controlador de umidade garantem a segurança dos alimentos durante a doação. Será implementado um controle rigoroso e total configuração para se adaptar a diversos casos de mercadoria.

O projeto utiliza o Arduino para interagir com os sensores de temperatura e umidade, controlar os atuadores (LEDs e buzzer) e fornecer uma interface para configuração e monitoramento do sistema por meio de telas LCD. Essa integração permite o controle rigoroso das condições de temperatura e umidade da carga de alimentos, garantindo a segurança durante o transporte e armazenamento.

## Requisitos

- Placa Arduino
- Sensor de temperatura (exemplo: TMP36)
- Sensor de umidade
- LEDs
- Buzzer
- Telas LCD
- Resistores
- Jumpers e cabos para conexão

## Dependências

- Biblioteca LiquidCrystal

## Instruções de Uso

1. Conecte os sensores de temperatura e umidade aos pinos correspondentes do Arduino, seguindo o esquema de ligação apropriado.
2. Conecte os LEDs e o buzzer aos pinos de saída configurados no código.
3. Conecte as telas LCD aos pinos correspondentes do Arduino.
4. Faça o upload do código fornecido para o Arduino.
5. Verifique se todas as conexões estão corretas e o sistema está energizado.
6. O monitoramento das condições de temperatura e umidade será exibido nas telas LCD.
7. Caso a temperatura ultrapasse os limites definidos (baixa ou alta), os LEDs e o buzzer serão acionados como alerta.
8. Ajuste os parâmetros de temperatura de acordo com as necessidades do transporte de alimentos, alterando as variáveis `TempBaixa` e `TempAlta` no código.
9. Monitore regularmente as leituras de temperatura e umidade exibidas nas telas LCD para garantir o transporte seguro dos alimentos.

## Resultados Esperados e Impacto

A solução proposta busca alcançar os seguintes resultados:

- Monitoramento preciso das condições ambientais dos alimentos.
- Alertas imediatos em caso de variações indesejadas de temperatura.
- Controle personalizado dos parâmetros do sistema para diferentes tipos de mercadorias.
- Melhoria da qualidade e segurança dos alimentos, evitando deterioração e contaminação.
- Eficiência operacional por meio da automação do monitoramento e controle.

Esses resultados positivos proporcionarão produtos mais seguros, reduzirão desperdícios, simplificarão as operações logísticas e fortalecerão a reputação da empresa.

## Código Fonte



Aqui está o código fonte utilizado no TinkerCad:

```cpp
// Carrega a Biblioteca LiquidCrystal
#include <LiquidCrystal.h>

// Define os pinos que serão utilizados para ligação ao display
LiquidCrystal LCD(12,11,5,4,3,2);

// Variáveis

int SensorTempPino=0;
int SensorUmidPino=1;
const int som = 6;
int porcem=0;


// Define o pino 8 para o alerta de temperatura baixa
int AlertaTempBaixa=8;
// Define o pino 13 para o alerta de temperatura alta
int AlertaTempAlta=13;

// Define temperatura baixa como 5 grau Celsius
int TempBaixa= 5;
// Define temperatura alta como acima de 40 graus Celsius
int TempAlta= 30;


void setup() 
{
  // Informa se os pinos dos LEDs são de entrada ou saída
  pinMode(AlertaTempBaixa, OUTPUT);  
  pinMode(AlertaTempAlta, OUTPUT);
  pinMode(som, OUTPUT);
	
  // Define LCD 16 colunas por 2 linhas
  LCD.begin(16,2);
  
  //Posiciona o cursor na coluna 0, linha 0;
  LCD.setCursor(0,0);
  
  // Imprime a mensagem no LCD
  LCD.print("Temper.:");

  // Imprime a mensagem no LCD
  LCD.print("Umidad.:");

  // Muda o cursor para a primeira coluna e segunda linha do LCD
  LCD.setCursor(0,1);
  
  // Imprime a mensagem no LCD
  LCD.print("      C      ");
  
  // Imprime a mensagem no LCD
  LCD.setCursor(14,1);
  LCD.print("%");
}

void loop()
{
   // Faz a leitura da tensao no Sensor de Temperatura
   int SensorTempTensao=analogRead(SensorTempPino);

   // Converte a tensao lida
   float Tensao=SensorTempTensao*5;
   Tensao/=1024;

   // Converte a tensao lida em Graus Celsius
   float TemperaturaC=(Tensao-0.5)*100;

   // Muda o cursor para a primeira coluna e segunda linha do LCD
   LCD.setCursor(0,1);

   // Imprime a temperatura em Graus Celsius
   LCD.print(TemperaturaC);
  
    
    // Faz a leitura da tensao no Sensor de Umidade 
    int SensorUmidTensao=analogRead(SensorUmidPino);
        
    // Converte a tensao lida em porcentagem
    float porcem=map(SensorUmidTensao,0,1023,0,100);
    
    // Muda o cursor para a segunda coluna e nona linha do LCD
    LCD.setCursor(8,1);
     
    // Imprime a umidade em porcentagem
    LCD.print(porcem);
     
  
  // Acende ou apaga os alertas luminosos de temperatura baixa e alta
  	if (TemperaturaC>=TempAlta) {
  		digitalWrite(AlertaTempBaixa, LOW);
  		digitalWrite(AlertaTempAlta, HIGH);
      	digitalWrite(som, HIGH);
    }
  	else if (TemperaturaC<=TempBaixa) {
  		digitalWrite(AlertaTempBaixa, HIGH);
  		digitalWrite(AlertaTempAlta, LOW);
      	d

igitalWrite(som, HIGH);
  	}
  	else {
  		digitalWrite(AlertaTempBaixa, LOW);
  		digitalWrite(AlertaTempAlta, LOW);
     	digitalWrite(som, LOW);
    }

  // Aguarda 1 segundo
  	delay(1000);
}  
```

Certifique-se de ter as bibliotecas necessárias instaladas em sua IDE do Arduino para garantir a compilação correta do código.

