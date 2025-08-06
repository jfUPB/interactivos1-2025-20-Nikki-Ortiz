# Unidad 2

## 🔎 Fase: Set + Seek

## ACTIVIDAD 1

### Documentación de Código (para enterder mejor y responder las preguntas)

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

**Funcionamiento por partes explicada desde el funcionamiento del código:**

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

> Nota: En este caso la actividad se presentó en forma de tablas debido a que "Notion" facilita la notación en markdown y se transfirió desde allí a github :)

## ACTIVIDAD 2
Implementando un semáforo con máquina de estados

### 1. Escribe el código que soluciona este problema en tu bitácora. (Documentado) 

```py

```



