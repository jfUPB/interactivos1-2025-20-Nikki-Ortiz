# Unidad 2

## 🔎 Fase: Set + Seek

## ACTIVIDAD 1

### Documentación de Código (para enterder mejor y responder las preguntas). 

```py
# - utime: Esto sirve para manejar el tiempo con precisión en milisegundos
from microbit import *
import utime

# Clase Pixel: representa un solo LED de la pantalla 
class Pixel:
    # Constructor que se ejecuta al crear un nuevo Pixel
    def __init__(self, pixelX, pixelY, initState, interval):
        self.state = "Init"           # Estado inicial del objeto (una máquina de estados)
        self.startTime = 0            # Marca de tiempo en la que empieza a contar el intervalo
        self.interval = interval      # Intervalo de tiempo (en ms) para los cambios de estado del pixel
        self.pixelX = pixelX          # Posición horizontal (columna) del píxel en el microbit (es un cuadrado 5x5)
        self.pixelY = pixelY          # Posición vertical (fila) del píxel
        self.pixelState = initState   # Estado de brillo inicial del píxel (0 = apagado, 9 = encendido)

    # Método que se debe llamar repetidamente para actualizar el comportamiento del pixel
    def update(self):

        # Si el estado actual es "Init", esto solo se ejecuta una vez, al comienzo
        if self.state == "Init":
            self.startTime = utime.ticks_ms()  # Guarda el tiempo actual como referencia de inicio
            self.state = "WaitTimeout"         # Cambia al siguiente estado (espera a que pase el intervalo)
            display.set_pixel(self.pixelX, self.pixelY, self.pixelState)  # Muestra el estado inicial del píxel en pantalla

        # Si el estado es "WaitTimeout", se revisa si ya pasó el intervalo de tiempo
        elif self.state == "WaitTimeout":
            # Calcula la diferencia entre el tiempo actual y el de inicio
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()  # Reinicia el tiempo de referencia para el próximo cambio

                # Alterna el estado del píxel: si estaba encendido (9), lo apaga (0); si estaba apagado, lo enciende
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9

                # Aplica el nuevo estado del pixel en los LEDs
                display.set_pixel(self.pixelX, self.pixelY, self.pixelState)

# Crea una instancia del pixel 1:
# - posición (0, 0)
# - estado inicial apagado (0)
# - intervalo de 1000 ms = 1 segundo
pixel1 = Pixel(0, 0, 0, 1000)

# Crea una instancia del pixel 2:
# - posición (4, 4)
# - estado inicial apagado (0)
# - intervalo de 500 ms = 0.5 segundos
pixel2 = Pixel(4, 4, 0, 500)

# Bucle principal que se ejecuta infinitamente
while True:
    # Actualiza ambos pixeles en cada iteración del bucle
    pixel1.update()
    pixel2.update()
```

### 1. ¿Cómo funciona este ejemplo?  

El programa que podemos ver en el ejemplo está diseñado para encender y apagar dos píxeles en la pantalla LED del micro:bit, cada uno con un intervalo de tiempo diferente. Utiliza una clase `Pixel` para establecer el comportamiento de un píxel que cambia de estado (encendido/apagado) de forma periódica.  

**Funcionamiento por partes explicada desde el funcionamiento del código:**. 

1.1 Se definen dos objetos de tipo `Pixel`:

   -  `pixel1` en la posición (0,0), cambia cada 1000 ms (1 segundo).
   -  `pixel2` en la posición (4,4), cambia cada 500 ms (0.5 segundos).

1.2 Cada objeto comienza en estado "Init", donde inicializa su temporizador (`startTime`) y se dibuja por primera vez en la pantalla.  

1.3 Luego entra en estado "WaitTimeout", donde espera a que pase el tiempo definido por `interval`.  

1.4 Una vez que pasa ese tiempo:  

  - Cambia el brillo del píxel: si estaba encendido (valor 9), lo apaga (valor 0), y viceversa.
  - Reinicia el temporizador para repetir el proceso.

### 2. ¿Cuáles son los estados en el programa?  

Después de analizar el código logré identificar 2 estados, los cuales son:   

| Estado          | Descripción                                                                      |
| --------------- | -------------------------------------------------------------------------------- |
| `"Init"`        | Estado inicial: configura el tiempo de inicio y enciende el píxel.               |
| `"WaitTimeout"` | Espera a que transcurra el tiempo (`interval`) para cambiar el estado del píxel. |


### 3. ¿Cuáles son los eventos/inputs en el programa?  

En este caso este programa no reponde a eventos externos sino internos (no recibe nada del ecterior por medio del port). Por lo cual, dichos eventos serían:  


| Evento              | Descripción                                                                   |
| --------------------| ----------------------------------------------------------------------------- |
| Inicio del programa | Se crea cada objeto Pixel y se inicializa el primer estado.                   |
| Tiempo transcurrido | Cuando el tiempo actual supera el `interval`, se  realiza un cambio de estado.|


### 4. ¿Cuáles son las acciones en el programa?  

Estas son las acciones visibles o internas que realiza el programa:  

| Acción                                | ¿Cuándo ocurre?                                              |
| ------------------------------------- | ------------------------------------------------------------ |
| `display.set_pixel(x, y, brightness)` | Cuando el estado cambia (en `Init` o al alternar el brillo). |
| `self.startTime = utime.ticks_ms()`   | Al iniciar o reiniciar el temporizador.                      |
| Alternar `pixelState` entre 0 y 9     | Cuando se cumple el tiempo (`interval`).                     |

> Nota: En este caso la actividad se presentó en forma de tablas debido a que "Notion" facilita la notación en markdown y se transfirió desde allí a github :). 

## ACTIVIDAD 2
Implementando un semáforo con máquina de estados. 

### 1. Escribe el código que soluciona este problema en tu bitácora. (Documentado)   

```py
from microbit import *      
import utime                # Usa utime para trabajar con tiempo en milisegundos

ROJO = "Rojo"
VERDE = "Verde"
AMARILLO = "Amarillo"

# Posicion de los LEDs en Coordenadas (x, y) 
red_pos = (2, 0)     # LED rojo en la parte superior
yellow_pos = (2, 1)  # LED amarillo en el centro
green_pos = (2, 2)   # LED verde en la parte inferior

# Estado inicial del semáforo: comienza en rojo
current_state = ROJO

# Guarda el tiempo de inicio del estado actual
start_time = utime.ticks_ms()

# Función que apaga todos los LEDs del semáforo (pone brillo 0 en cada LED)
def clear_all():
    display.set_pixel(red_pos[0], red_pos[1], 0)
    display.set_pixel(yellow_pos[0], yellow_pos[1], 0)
    display.set_pixel(green_pos[0], green_pos[1], 0)

# Función principal que actualiza el estado del semáforo según el tiempo transcurrido
def update_traffic_light():
    global current_state, start_time  

    # Calcula cuántos milisegundos han pasado desde el inicio del estado actual
    elapsed = utime.ticks_diff(utime.ticks_ms(), start_time)

    if current_state == ROJO:
        clear_all()  # Apaga todos los LEDs
        display.set_pixel(red_pos[0], red_pos[1], 9)  # Enciende el LED rojo
        if elapsed >= 5000:  # Si han pasado 5 segundos (5000 ms)
            current_state = VERDE  # Cambia al estado verde
            start_time = utime.ticks_ms()  # Reinicia el temporizador

    elif current_state == VERDE:
        clear_all()
        display.set_pixel(green_pos[0], green_pos[1], 9)  # Enciende el LED verde
        if elapsed >= 3000:  # Si han pasado 3 segundos
            current_state = AMARILLO  # Cambia al estado amarillo
            start_time = utime.ticks_ms()  # Reinicia el temporizador

    elif current_state == AMARILLO:
        clear_all()
        display.set_pixel(yellow_pos[0], yellow_pos[1], 9)  # Enciende el LED amarillo
        if elapsed >= 1000:  # Si han pasado 1 segundo
            current_state = ROJO  # Regresa al estado rojo
            start_time = utime.ticks_ms()  # Reinicia el temporizador

# Bucle principal del programa: actualiza el semáforo en cada ciclo
while True:
    update_traffic_light()  # Llama a la función que controla la lógica del semáforo
    sleep(100)  # Espera 100 milisegundos antes de la siguiente actualización
```

> Nota: Se verificó el funcionamiento del programa con el simulador de micro:bit

### 2. Identifica los estados, eventos y acciones en tu código.  

2.1 Estados del sistema:   

- ROJO: El LED rojo está encendido.
- VERDE: El LED verde está encendido.
- AMARILLO: El LED amarillo está encendido.

2.2 Eventos que provocan cambios de estado:  

- Desde ROJO, si han pasado 5 segundos (5000 ms), cambia a VERDE.
- Desde VERDE, si han pasado 3 segundos (3000 ms), cambia a AMARILLO.
- Desde AMARILLO, si han pasado 1 segundo (1000 ms), cambia a ROJO.

2.3 Acciones realizadas en cada estado:  

- **Cuando el estado es ROJO:**
Apaga todos los LEDs (clear_all()).
Enciende el LED rojo con brillo 9 (display.set_pixel(red_pos[0], red_pos[1], 9)).

- **Cuando el estado es VERDE:**
Apaga todos los LEDs.
Enciende el LED verde con brillo 9 (display.set_pixel(green_pos[0], green_pos[1], 9)).

- **Cuando el estado es AMARILLO:**
Apaga todos los LEDs.
Enciende el LED amarillo con brillo 9 (display.set_pixel(yellow_pos[0], yellow_pos[1], 9)).  

## ACTIVIDAD 3. 

### 1. Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.  

El programa desarrollado logra un comportamiento concurrente porque responde al mismo tiempo a dos tipos de eventos:

• Por un lado, los temporizados (cambios de imagen controlados por un cronómetro establecido en milisegundos).
• Por otro, las acciones del usuario (como cuando se presiona el botón A).

Aunque el micro:bit ejecuta instrucciones en orden y no es capaz de realizar tareas en paralelo como tal (como cuando se mencionó en clase que poner un sonido/audio en el código podía estropear el resto de las acciones porque se iba a quedar sonando), el diseño esta basado en una  máquina de estados, junto con la revisión constante de los temporizadores y del botón, permite simular esa concurrencia. El sistema sigue mostrando imágenes en secuencia, pero si el usuario presiona el botón A, se interrumpe de inmediato para responder, sin tener que esperar a que se cumpla el tiempo del cronómetro.  

### 2. Identifica los estados, eventos y acciones en el programa.  

2.1 Estados: 
	- STATE_INIT
	- STATE_HAPPY
	- STATE_SMILE
	- STATE_SAD

2.2 Eventos:  
	- utime excede el intervalo del estado actual 
	- button_a.was_pressed()

2.3 Acciones: 
	- Mostrar imágenes (Image.HAPPY, Image.SMILE, Image.SAD)
	- Actualizar el estado actual y el start_time
	- Asignar el nuevo intervalo

### 3. Describe y aplica al menos 3 vectores de prueba para el programa. 
Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.  

**3.1 Vector de Prueba 1:**
- Condiciones iniciales: Estado = STATE_HAPPY, el botón A es presionado antes de que pasen 1500 ms.
- Evento: button_a.was_pressed() == True
- Resultado esperado:
	- Imagen: Image.SAD
	- Estado nuevo: STATE_SAD
	- Intervalo: 2000 ms
- Resultado obtenido: coincide con el comportamiento esperado. 

**3.2 Vector de Prueba 2:**
- Condiciones iniciales: Estado = STATE_SMILE, tiempo transcurrido = 1000 ms, no se presiona el botón A.
- Evento: utime.ticks_diff(...) > interval
- Resultado esperado:
	- Imagen: Image.SAD
	- Estado nuevo: STATE_SAD
	- Intervalo: 2000 ms
- Resultado obtenido: pasa el vector de prueba. 

**3.3 Vector de Prueba 3:**
- Condiciones iniciales: Estado = STATE_SAD, el botón A es presionado antes de los 2000 ms.
- Evento: button_a.was_pressed() == True
- Resultado esperado:
	- Imagen: Image.SMILE
	- Estado nuevo: STATE_SMILE
	- Intervalo: 1000 ms
- Resultado obtenido: el sistema responde como se espera





