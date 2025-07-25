# Unidad 1

## 🤔 Fase: Reflect  

## ACTIVIDAD 07 - Parte 1: recuperación de conocimiento (Retrieval Practice)

### 1. Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.

Estímulos que se activan mediante interacción usuario-máquina, la influencia humana en las bases de los programas para lograr ciertos niveles de autonomía por parte de la máquina y  el uso de tecnologías con dispositivos de salida, entrada y un proceso de por medio que al integrarse permiten obtener un resultado que permita comunicar y evocar emociones al usuario mientras este es partícipe de la experiencia  

### 2. Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output? 

En este sistema los imputs son conectar el micro:bit, pulsar 'A' o 'B y el envío de caracteres por medio del puerto serial; por el lado de los procesos, debe crear un canvas y el sistema debe leer la información que está recibiendo a través del port, de acuerdo con esa información interpretar el movimiento que tendrá el círculo en el eje X, en concordancia con la dirección asignada para 'A' y para 'B' haciendo uso de una resta o una suma a la posición actual del círculo para lograr dicho movimiento; finalmente, en el caso de los outputs estaría mostrar en la interfaz el canvas creado con el tamaño establecido, generar el circulo en la posición que se le asigno, y mostrar el movimiento del círculo reflejado, así como también, desconectar el microbit o conectarlo de nuevo.

### 3. ¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?  

La línea de uart.write('A') se encarga de enviar el carácter 'A' del micro:bit a la computadora por medio del port, para que el computador reciba este carácter por medio del port, se necesita la línea let dataRx = port.read(1);  y así este podría ejecutar la siguiente línea del programa en p5.js que sería (en el caso de la actividad 6, por ejemplo) if (dataRx == "A" && dirX > 50) la cual procesa el carácter A como una instrucción relacionada con la dirección del círculo.  

### 4. ¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?    

En el diseño/arte realizado de manera tradicional el artista realiza todo el trabajo de manera manual, con el uso de herramientas rudimentarias, y valga la redundancia, tradicionales, como lo serían los pinceles, la pintura, los grafitos, entre otros; intentando plasmar en un Canvas o espacio sentimientos o intenciones. Sin embargo, aunque el diseño/arte generativo también tiene la intención de transmitir algo, este pasa a emplear herramientas tecnológicas que crean una relación entre el artista y una máquina, facilitando la producción en masa, la personalización, la creatividad y la automatización de procesos mediante guías y ordenes que le dan a la máquina un grado de autonomía deseado según lo que se quiera producir.  

### 5. Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.    

FALTA 

## Parte 2: reflexión sobre tu proceso (Metacognición)

### 1. ¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?  

Con toda sinceridad creo que un poco de ambas, ya que en lo personal siento que debo repasar más los conceptos de programación para poder progresar de manera correcta en esta materia, razón que está relacionada con mi situación de salud, lo cual es frustrante, pero aun así es un reto personal que debe ser superado, no solo por interés académico, no quiero aprender a hacer las cosas porque si, sin interiorizar conocimientos, quiero más bien todo lo contrario, aprender lo más que pueda de esta materia, porque sé que lo voy a necesitar, sé que lo voy a usar, es de mi interés total las temáticas trabajadas y a trabajar y me esforzaré por mejorar en la parte práctica y de conocimiento ahora que apenas estamos empezando

### 2. Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?  

En la primera clase donde usamos el microbit y entendi que respondía a interacciones 



### Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?  

### El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?
