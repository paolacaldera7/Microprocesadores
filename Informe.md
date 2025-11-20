# ONDA TRIANGULAR

# Este codigo funciona para generar una onda triangular mediante los comandos descritos proximamente. Empezamos importando los comandos de la libreria "machine" como por ejemplo, los pines, PWM, ADC y utime. 



```python
from machine import Pin, PWM , ADC
import utime

# Configura PWM en GPIO15
pwm = PWM(Pin(15))
pwm.freq(1000)  # Frecuencia fija

# Parámetros de la onda
steps = 50       # Número de niveles por subida/bajada
delay = 50       # Tiempo entre pasos (ms)
max_duty = 65535 # Máximo valor de duty cycle

#Entrada Analogica
adc = ADC(Pin(26))
# Funcion para convertir duty a float
def duty_to_float(duty):
    return duty / max_duty

# Funcion para convertir duty a voltaje
def duty_to_voltaje(duty):
    return (duty / max_duty) * 3.3
# Generador de onda triangular discreta
def triangular_wave():
    while True:
        # Subida
        for i in range(steps):
            duty = int((i / steps) * max_duty)
            pwm.duty_u16(duty)
            utime.sleep_ms(delay)
        # Bajada
        for i in range(steps, -1, -1):
            duty = int((i / steps) * max_duty)
            pwm.duty_u16(duty)
            utime.sleep_ms(delay)
            valor = adc.read_u16()
            voltaje = valor * 3.3 / 65535
            utime.sleep_ms(10)
            print(duty_to_voltaje(duty))

# Ejecutar
triangular_wave()

```
 