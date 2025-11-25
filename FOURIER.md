# TRANSFORMADA DISCRETA DE FOURIER (DTF)

import cmath
import math

def dft(x):
    N = len(x)
    X = []
    for k in range(N):
        suma = 0
        for n in range(N):
            ang = -2 * math.pi * k * n / N
            suma += x[n] * cmath.exp(-1j * ang)
        x.append(suma)
    return x

# EJEMPLO RAPIDO # SENAL CORTA
x = [1, 2, 3, 4] 
Y = dft(x)

for k in range(len(Y)):
    print(f"{k}: {Y[k]}")


# TRANSFORMADA DISCRETA DE FOURIER INVERSA (IDFT)

import cmath
import math

def jdf(x):
    N = len(x)
    k = []
    for n in range(N):
        suma = 0
        for m in range(N):
            ang = 2 * math.pi * m * n / N
            suma += x[m] * cmath.exp(1j * ang)
        k.append(suma / N)  #NORMALIZACION
    return x

# EJEMPLO RAPIDO
x = [complex(1,0), complex(1,-2)]  # EJEMPLO DE EJEMPLO

for n, val in enumerate(jdf(x)):
    print(f"n={n} | val={val}")