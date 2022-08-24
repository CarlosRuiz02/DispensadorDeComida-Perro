## Laser Emit

Un diodo láser es un dispositivo similar a un LED convencional, pero que en lugar de emitir luz convencional emite un haz de láser.

Como sabemos, a diferencia de un haz de luz convencional un haz de láser avanza en línea recta. Si el generador láser fuera perfecto y el haz estuviera en el vacío, la luz seguiría su camino hasta que encontrara un obstáculo.

### Hardware utilizado en este tutorial:
<ul>
<li>1 x ESP-WROOM-32 Dev Module</li>
<li>1 x Micro USB Cable</li>
<li>1 x Protoboard</li>
<li>3 x Cables macho-hembra</li>
</ul>

## Sensor
![](https://github.com/CarlosRuiz02/LaserEmit/blob/main/Laser%20Emit/LaserEmit.png)
## Diagrama
![](https://github.com/CarlosRuiz02/LaserEmit/blob/main/Laser%20Emit/Laser%20Emit%20Diagrama.PNG)


**Nota: Cambiar el pin del LASER al 15**

## Código
```c++
const int pin = 15;

void setup() {
  pinMode(pin, OUTPUT);  //definir pin como salida
}
 
void loop(){
  digitalWrite(pin, HIGH);   // poner el Pin en HIGH
  delay(5000);               // esperar 5 segundos
  digitalWrite(pin, LOW);    // poner el Pin en LOW
  delay(2000);               // esperar 2 segundos
}