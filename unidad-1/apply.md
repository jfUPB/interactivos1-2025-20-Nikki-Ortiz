# Unidad 1

## 🛠 Fase: Apply

## ACTIVIDAD 05  

- INPUTS: Clic en el botón "Connect to micro:bit" en la página, pulsar el botón 'A'. Envío de caracteres 'A' o 'N' a través del puerto serial de acuerdo con la acción realizada.    
- OUTPUTS: En la interfaz p5.js debe aparecer un rectángulo en el centro que cambia de color según el código: rojo o verde. Adicionalmente, debe aparecer el "Connect to micro:bit" o "Disconnect" según el estado del dispositivo.   
- PROCESOS: Este apartado está dividido en los procesos del micro:bit y los procesos de la consola de p5.js.  

    1. MICRO:BIT -> Inicializa la comunicación UART de acuerdo con la velocidad de transmisión de datos establecida (115200), entra en un bucle (while True) en donde los ciclos "if" y "else" establecen que si se presiona el botón A, envía       el carácter 'A' por el puerto serial, y si no se presiona 'A', entonces debe enviar 'N' y esperar 100 milisegundos antes de repetir el ciclo.  
       
    2. P5.JS -> Crea un lienzo en la interfaz de 400x400, muestra un botón que permita conectar o desconectar al puerto serial, Si hay datos disponibles en el puerto serial (if (port.availableBytes() > 0)) entonces procesa los datos, si recibe "A" entonces dibuja un cuadro rojo, de lo contrario, si no se presionó o está presionando 'A', debería tomarlo como 'N' gracias al ciclo de "else" y mostrar en pantalla un cuadrado verde, para después actualizar de manera continua el fondo y el estado del botón de connect de acuerdo con el port.  
 
       
## ACTIVIDAD 06 



