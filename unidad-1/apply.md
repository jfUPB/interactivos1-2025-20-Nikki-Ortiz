# Unidad 1

## 🛠 Fase: Apply

## ACTIVIDAD 05  

- INPUTS: Clic en el botón "Connect to micro:bit" en la página, pulsar el botón 'A'. Envío de caracteres 'A' o 'N' a través del puerto serial de acuerdo con la acción realizada.    
- OUTPUTS: En la interfaz p5.js debe aparecer un rectángulo en el centro que cambia de color según el código: rojo o verde. Adicionalmente, debe aparecer el "Connect to micro:bit" o "Disconnect" según el estado del dispositivo.   
- PROCESOS: Este apartado está dividido en los procesos del micro:bit y los procesos de la consola de p5.js.  

    1. MICRO:BIT -> Inicializa la comunicación UART de acuerdo con la velocidad de transmisión de datos establecida (115200), entra en un bucle (while True) en donde los ciclos "if" y "else" establecen que si se presiona el botón A, envía       el carácter 'A' por el puerto serial, y si no se presiona 'A', entonces debe enviar 'N' y esperar 100 milisegundos antes de repetir el ciclo.  
       
    2. P5.JS -> Crea un lienzo en la interfaz de 400x400, muestra un botón que permita conectar o desconectar al puerto serial, Si hay datos disponibles en el puerto serial (if (port.availableBytes() > 0)) entonces procesa los datos, si recibe "A" entonces dibuja un cuadro rojo, de lo contrario, si no se presionó o está presionando 'A', debería tomarlo como 'N' gracias al ciclo de "else" y mostrar en pantalla un cuadrado verde, para después actualizar de manera continua el fondo y el estado del botón de connect de acuerdo con el port.  
 
       
## ACTIVIDAD 06 

### LINK DEL CÓDIGO: 
https://editor.p5js.org/Nikki-Ortiz/sketches/XaK1RuZ-A

### CÓDIGO DEL PROGRAMA EN P5.JS: 

```js
let port;
let connectBtn;
let connectionInitialized = false;
let dirX = 50;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);   
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A" && dirX > 50) { 
       dirX -= 30;
      } else if (dataRx == "B" && dirX < 350) {
       dirX += 30;
      }
    }

    ellipseMode(RADIUS);
    ellipse (dirX, height / 2, 50, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
```
### CÓDIGO DEL PROGRAMA EN MICRO:BIT  

```py
# Imports go at the top
from microbit import *
uart.init(baudrate=115200)

# Code in a 'while True:' loop repeats forever
while True:
    if (button_a.is_pressed()):
        uart.write('A')
        
    if (button_b.is_pressed()):
        uart.write('B')
        
    else:
        uart.write('N')

    sleep(100)
```



