## Dispensador de comida para perros

En este proyecto, se verá los materiales, el procedimiento y las herramientas de software necesarias para poder crear un dispensador de comida autonomo para nuestras mascotas, aunque se menciona para perros (que en este caso para ellos va enfocado), también se puede útilizar para gatos, pájaros, etc.

### Hardware utilizado en este tutorial:
<ul>
<li>1 x ESP-WROOM-32 Dev Module</li>
<li>1 x Modulo de reloj DS1302</li>
<li>1 x Micro USB Cable</li>
<li>1 x Protoboard</li>
<li>n x Cables macho-hembra</li>
<li>n x Cables macho</li>
</ul>

## Modulo de reloj DS1302
![](https://github.com/CarlosRuiz02/DispensadorDeComida-Perro/blob/main/Dispensador-comida/Figs/RTC.jpg)
## Diagrama
![](https://github.com/CarlosRuiz02/DispensadorDeComida-Perro/blob/main/Dispensador-comida/Figs/AlimentadorDiagrama.png)

**En este poyecto se utilizó el modulo RTC DS1302 pero pueden utilizar cualquier otro RTC e incluso el NTC del ESP32**

El código tiene una línea comentada, la cuál sirve para actualizar o modificar la hora del Modulo, en el if inferior podremos cambiar las horas en las que se les dará de comer a los cachorros.

## Código
```c++
#include <virtuabotixRTC.h> //Libreria
#include <ESP32Servo.h>
Servo servoMotor;

virtuabotixRTC myRTC(21, 22, 23); // Si cambiamos los PIN de conexión, debemos cambiar aquí tambien

void setup() {
  Serial.begin(9600);

  // Para ajustar la fecha y hora, debemos utilizar el siguiente formato:
  // segundos, minutos, horas, dia de la semana, numero de día, mes y año
  //myRTC.setDS1302Time(00, 12, 23, 2, 23, 8, 2022); // SS, MM, HH, DW, DD, MM, YYYY
  /* después de ajustar la hora la linea de arriba se debe comentar o eliminar
   *  para que la fecha y hora quede grabada
  */
  // La configuración de fecha y hora ha sido ajustada
}

void loop() {
  // Esta función actualiza las variables para obtener resultados actuales
  myRTC.updateTime();

  // Se imprime el resultado en el Monitor Serial
  Serial.print("Fecha y hora actual: ");
  Serial.print(myRTC.dayofmonth); // Se puede cambiar entre día y mes si se utiliza el sistema Americano
  Serial.print("/");
  Serial.print(myRTC.month);
  Serial.print("/");
  Serial.print(myRTC.year);
  Serial.print(" ");
  Serial.print(myRTC.hours);
  Serial.print(":");
  Serial.print(myRTC.minutes);
  Serial.print(":");
  Serial.println(myRTC.seconds);

  // Un pequeño delay para no repetir y leer más facil
  delay(1000);

  if(int(myRTC.hours)==8 || int(myRTC.hours)==13 || int(myRTC.hours)==23){
    if(int(myRTC.minutes)==31 ){
      if(int(myRTC.seconds)==20){
        servoMotor.attach(15);
      int i;
      for (i=0;i<3;i++){
        servoMotor.write(0);
        delay(1000);
        servoMotor.write(90);
        delay(500);
      }
      servoMotor.detach();
      }
    }  
  }
}