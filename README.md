# Li-Raspberry-pico
## Practica 0: Encender un led
### Codigo
```
from machine import Pin
import time

led = Pin("LED", Pin.OUT)  # "LED" es un alias al pin 25 interno

while True:
    led.toggle()
    time.sleep(0.5)
```
### Ejecucion

## Practica 2: Desplegar hora de internet
### Codigo
```
import network
import time
import ntptime

# Configuración de Wi-Fi
ssid = "TecNM-ITT"  # Nombre de tu red Wi-Fi
password = ""  # Contraseña de tu red Wi-Fi, si la tiene

# Conectar a la red Wi-Fi
wifi = network.WLAN(network.STA_IF)
wifi.active(True)
wifi.connect(ssid, password)

# Esperar a que la conexión Wi-Fi sea exitosa
while not wifi.isconnected():
    print("Conectando a Wi-Fi...")
    time.sleep(1)

print("Conectado a Wi-Fi")

# Obtener la hora de Internet usando NTP
try:
    ntptime.settime()  # Esto ajusta el reloj del sistema
    print("Hora sincronizada con NTP")
except Exception as e:
    print("Error al sincronizar la hora: ", e)

# Mostrar la hora actual en la consola serial (zona horaria UTC-8)
while True:
    # Obtener la hora del sistema (en UTC)
    current_time = time.localtime()

    # Ajustar la hora a UTC-8 (zona horaria del Pacífico)
    current_time_pacific = time.localtime(time.mktime(current_time) - 8 * 3600)  # Restar 8 horas

    print("Hora actual (Pacífico):", current_time_pacific)
    time.sleep(60)  # Actualizar cada minuto
```
### Ejecucion

