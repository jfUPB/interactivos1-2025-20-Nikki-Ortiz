# Unidad 1

## 🔎 Fase: Set + Seek

## ACTIVIDAD 01

### ¿Qué es un sistema físico interactivo?  

Es un intercambio de información o una relación entre un sistema (que tiene imputs, outputs y procesos) y el mundo físico que permite materializar ideas y diseños definidos para que el usuario interactúe con ellos. Es decir, un Sistema Físico Interactivo hace uso de las tecnologías disponibles (sobre todo herramientas TIC, programación y tecnologías digitales y de sensórica) para conceptualizar, diseñar e implementar una experiencia que conecte y genere emociones con el usuario                                                                                                                                                                                                                                                                                                                                                                                                                    
### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?   

Como persona que desea irse por la rama de Experiencias Interactivas creo que esta clase es ideal para aprender a transformar algo sencillo del mundo físico en una experiencia que haga que el usuario se conecte con las ideas y conceptos que se buscan transmitir, inclusive, busca también realzar y acompañar proyectos que ya existen, dándoles un valor agregado, estando presente en procesos como la captura de movimiento para juegos y animaciones, el branding y el diseño de producto, el cine y la música, el marketing, entre otras cosas (ej. escuchar una canción de Aurora vs. Escuchar la misma canción, pero con una interpretación generativa que crea arte a partir de las vibraciones de la canción). Por lo cual, creo firmemente que los Sistemas Físicos Interactivos poco a poco empiezan a integrarse en nuestro día a día, toman relevancia y son una muestra de a dónde se encamina el futuro.

## ACTIVIDAD 02

### ¿Qué es el diseño/arte generativo?  

El arte generativo es una práctica que se vale de un sistema con cierto grado de autonomía, en el cuales definen unas reglas, en algunos casos por medio de códigos que contienen instrucciones que facilitaran la realización de una obra (uno de los ejemplos de arte generativo muestra por ejemplo como por medio del código se asignan formas y colores para hacer arte abstracto). Siendo así como se basa la generación de productos y comunicaciones basadas en datos, influencias sistemáticas y prográmicas multifacéticas 

### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?  

El diseño/arte generativo en muy útil en el perfil profesional porque proporciona al usuario experiencias únicas, innovativas y automatizadas, aumentando las posibilidades en el factor de personalización y mejora el factor de la carga de trabajo sin recurrir a otras herramientas controversiales que hacen que la carga de trabajo disminuya de manera poco ética; no afecta la creatividad y mejora el ingenio a la  hora de inventar nuevas experiencias multifaceticas, proviendo narrativas dinamicas, automatización de enternos visuales, parametrizaciones, entre otras cosas

## ACTIVIDAD 03

### En este sistema físico interactivo identifica los inputs, outputs y el proceso.  

Se dividen en los imputs, outputs y procesos del micro.bit y luego de la computadora por separado

### MICRO.BIT:
 
- Inputs: Los botones, agitar, dar amor 
- Outputs: Enviar ABC por computadora, muestra en pantalla 
- Procesos: Esperar por botones o movimiento para que, según lo detectado, envíe una letra a la pantalla. Si recibe amor, entonces debería mostrar una secuencia de imágenes según lo programado.

### COMPUTADORA (p5.js en navegador)

- Inputs: Datos enviados por el micro.bit por medio del cable. Clic en el botón “Connect to micro:bit”, clic en el botón “Send Love”
- Outputs: Dibuja un círculo de color en función de la letra recibida. Muestra la letra recibida en pantalla. Envía el patrón al Micro:bit si haces clic en “Send Love”
  
- Procesos: El usuario conecta el micro:bit por cable, ingresa el código correspondiente, lo conecta en la web, Si micro:bit envía datos, p5.js debería leer y cambiar el color del círculo según el valor y mostrar la letra en pantalla, si el usuario le da clic a "send love" el computador debe mandar la orden al micro.bit para mostrar la secuencia de imágenes.

## ACTIVIDAD 04

### ENLANCE AL CÓDIGO:  
https://editor.p5js.org/Nikki-Ortiz/sketches/LLL2ETBI-

### CÓDIGO:  

```js  

let t = 0;
let ampli, frec, vel, yuca;
let colores;
let tm;

function setup() {
  createCanvas(600, 400);
  background(10);
  noFill();
  
  mostrarGrafica();
  
  
}

function draw() {
  
  stroke(colores);
  let x = t % width;
  let y = sin(t * frec) * ampli + yuca;
  strokeWeight(tm);
  point(x,y);
  
  t += vel;
  
  if(frameCount % 240 === 0){
    mostrarGrafica();
  }  
}

function mostrarGrafica(){
  ampli = random(20, height / 2 - 20);
  frec = random(0.005, 0.05);
  vel = random(0.5, 2);
  yuca = random(height / 4, (3 * height) / 4);
  colores = color(random(150, 255), random(100, 255), random(100, 255), 180);
  tm = random(2,8);
  
}

```

### RESULTADO:  

<img width="2555" height="1392" alt="Captura de pantalla 2025-07-22 190214" src="https://github.com/user-attachments/assets/75d5702d-a87a-4d09-9be9-fb8915695851" />


