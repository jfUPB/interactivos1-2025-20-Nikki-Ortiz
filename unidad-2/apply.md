# Unidad 2  

## 🛠 Fase: Apply  

### ACTIVIDAD 4  

Construye un diagrama detallado de la máquina de estados, incluyendo estados, eventos, transiciones y acciones. 

<img width="1920" height="1080" alt="STATE_INNIT" src="https://github.com/user-attachments/assets/2da7aeae-a485-4a9c-b149-99961d61da8a" />  

[Canva Version](https://www.canva.com/design/DAGvc-xj-YM/kvvKXuUbzHlT-rb_i8mcHg/edit?utm_content=DAGvc-xj-YM&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)  


### ACTIVIDAD 5  


**5.1 CÓDIGO:**

```py
# Imports go at the top
from microbit import *
import utime
import music

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2

current_state = STATE_INIT
BOMB_INTERVAL = 20000
armed_start_time = 0
remaining_time = BOMB_INTERVAL

def show_time(ms):
    seconds = ms // 1000
    for digit in str(seconds):
        display.show(digit)
        sleep(400)


# Code in a 'while True:' loop repeats forever
while True:

    if current_state == STATE_INIT:
        display.show(Image.SAD)
        sleep(1000)
        current_state= STATE_CONFIG
        display.clear()

    elif current_state == STATE_CONFIG:  
        show_time(BOMB_INTERVAL)
        
        if button_a.was_pressed() and BOMB_INTERVAL < 60000:
            BOMB_INTERVAL += 1000
            display.show(Image.ARROW_N)
            sleep(300)
            
        elif button_b.was_pressed() and BOMB_INTERVAL > 10000:
            BOMB_INTERVAL -= 1000
            display.show(Image.ARROW_S)
            sleep(300)
            
        elif accelerometer.was_gesture('shake'):
            current_state = STATE_ARMED
            armed_start_time = utime.ticks_ms()
            remaining_time = BOMB_INTERVAL
            display.clear()
            
        sleep(100)
        
    elif current_state == STATE_ARMED:
        now = utime.ticks_ms()
        elapsed = utime.ticks_diff(now,armed_start_time)
        remaining_time = BOMB_INTERVAL - elapsed

        if remaining_time > 0:
            show_time(remaining_time)
        else:
            display.clear()
            display.show(Image.SKULL)
            music.play(music.WAWAWAWAA)
            sleep(2000)
            display.clear()
            current_state = STATE_CONFIG
            BOMB_INTERVAL = 20000
            continue

        if pin_logo.is_touched():
            current_state = STATE_CONFIG
            BOMB_INTERVAL = 20000
            display.clear()

        sleep(100)
```
----


**5.2 VECTORES DE PRUEBA:**  

---- 

Vector de Prueba 1: (INIT antes de paasar a CONFIG) 
  
- Condiciones iniciales: Estado = `STATE_INIT`, micro\:bit recién encendido.
- Evento: Realmente no hay evento, el micro:bit solo esta encendido
- Resultado esperado:
   - Imagen: `Image.SAD` durante 1000 ms. (Esto para saber que esta en el estado innit según el codigo)
   - Estado nuevo: `STATE_CONFIG`.
   - Intervalo: `BOMB_INTERVAL = 20000 ms`.
- Resultado obtenido:** Coincide con el comportamiento esperado.

----

Vector de Prueba 2:  (corresponde al evento de precionar A y que aumente el intervalo)  
 
- Condiciones iniciales: Estado = `STATE_CONFIG`, `BOMB_INTERVAL = 20000 ms`.
- Evento: `button_a.was_pressed() == True`.
- Resultado esperado:
   - Imagen: `Image.ARROW_N`. (aparece una flecha para indicar que el valor está aumentando) 
   - Estado nuevo: `STATE_CONFIG`.
   - Intervalo: `BOMB_INTERVAL = 21000 ms`.
- Resultado obtenido: Coincide con el comportamiento esperado.

> Nota: En el evento de precionar A hay un condicional de que no se puede disminuir a más de 60.000

----

Vector de Prueba 3:  (corresponde al evento de precionar B y que disminuya el intervalo)  

- Condiciones iniciales: Estado = `STATE_CONFIG`, `BOMB_INTERVAL = 20000 ms`.
- Evento: `button_b.was_pressed() == True`.
- Resultado esperado:
   - Imagen: `Image.ARROW_S`. (aparece una flecha para indicar que el valor está disminuyendo)
   - Estado nuevo: `STATE_CONFIG`.
   - Intervalo: `BOMB_INTERVAL = 19000 ms`.
- Resultado obtenido: Coincide con el comportamiento esperado.

> Nota: En el evento de precionar B hay un condicional de que no se puede disminuir a menos de 10.000

----

Vector de Prueba 4: (Activar la bomba con SHAKE)

- Condiciones iniciales: Estado = `STATE_CONFIG`, `BOMB_INTERVAL = 20000 ms`.
- Evento: `accelerometer.was_gesture('shake') == True`.
- Resultado esperado:
   - Imagen: Pantalla limpia.
   - Estado nuevo: `STATE_ARMED`.
   - Intervalo: `BOMB_INTERVAL` conservado (20000 ms).
- Resultado obtenido: Coincide con el comportamiento esperado.

----

Vector de Prueba 5: (Esperar los segundos hasta que el Countdown = 0 y activar el sonido cuando la bomba explota)

- Condiciones iniciales: Estado = `STATE_ARMED`, `BOMB_INTERVAL = 5000 ms`.
- Evento: Esperar hasta que `remaining_time <= 0`.
- Resultado esperado:
   - Imagen: `Image.SKULL`.
   - Sonido: `music.WAWAWAWAA`.
   - Estado nuevo: `STATE_CONFIG`.
   - Intervalo: `BOMB_INTERVAL = 20000 ms`.
- Resultado obtenido: Coincide con el comportamiento esperado.

> Nota: Cuando el Countdown esta en proceso no se trata solo de esperar a que llegue a cero para que pase al otro estado, sino que tambien se debe esperar el segundo (1000) entre número y número

----

Vector de Prueba 6: (Corresponde a volver al estado de config después de usar el botón TOUCH)

- Condiciones iniciales:** Estado = `STATE_ARMED`, `BOMB_INTERVAL = 15000 ms`.
- Evento: `pin_logo.is_touched() == True`.
- Resultado esperado:
   - Imagen: Pantalla limpia.
   - Estado nuevo: `STATE_CONFIG`.
   - Intervalo: `BOMB_INTERVAL = 20000 ms`.
- Resultado obtenido: Coincide con el comportamiento esperado.

----

> Notita final: Por alguna razón Git me está removiendo los espacios y se ve todo pegado, ya intente todo tipo de markdown pero como no funcionó te separo las cositas con los separadores (----) okay? :(
