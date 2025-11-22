# Laboratorio 5 Procesamiento de señales
# Variabilidad de la Frecuencia Cardíaca (HRV) y balance autonómico
## Docente: Erick Javier Arguello Prada
## Integrantes:
## ·Liseth Yuliana Clavijo 
## ·Maria Camila Rodriguez
## ·Adriana Valentina Alarcon 
## Fecha: Noviembre 2025
# Introduccion: 
La variabilidad de la frecuencia cardíaca (HRV, por sus siglas en inglés) es uno de los indicadores no invasivos más utilizados para evaluar el estado funcional del sistema nervioso autónomo, específicamente la interacción entre las ramas simpática y parasimpática. A partir de la señal electrocardiográfica (ECG), es posible obtener la serie de intervalos R-R y analizar sus fluctuaciones para identificar cambios en el balance autonómico asociados a diferentes condiciones fisiológicas y cognitivas.

En esta práctica se adquiere y procesa una señal ECG en dos escenarios: un estado de reposo absoluto y un estado de lectura en voz alta. Estas dos condiciones permiten comparar cómo la activación simpática y la modulación vagal varían ante un estímulo que involucra atención, respiración modificada y actividad verbal. Para ello, se realiza un preprocesamiento digital de la señal mediante el diseño e implementación de un filtro IIR, seguido de la detección de picos R y el cálculo de los intervalos R-R. Posteriormente, se evalúan parámetros temporales de la HRV, como la media de los intervalos y su desviación estándar (SDNN), y se construyen diagramas de Poincaré para estimar índices de actividad simpática (CSI) y parasimpática (CVI).

Este laboratorio permite integrar conocimientos de procesamiento digital de señales y fisiología cardiovascular, reforzando la comprensión del comportamiento dinámico del corazón bajo influencias autonómicas y fortaleciendo habilidades de análisis cuantitativo mediante herramientas computacionales.


# Sistema Nervioso Autónomo (Simpático y Parasimpático)

El sistema nervioso autónomo quien regula funciones involuntarias esenciales para la supervivencia, como la frecuencia cardíaca, la presión arterial y la respiración. Está compuesto por dos ramas principales:

<img width="474" height="430" alt="image" src="https://github.com/user-attachments/assets/0b1d9e93-09a1-4691-b20b-d1a25ed95bd4" />



# Sistema Nervioso Simpático (SNS)

Se activa en situaciones de alerta o estrés. Sus efectos sobre el corazón incluyen:

-Aumento de la frecuencia cardíaca (taquicardia).
-Reducción de la variabilidad de la frecuencia cardíaca.
-Incremento de la contractilidad miocárdica.
-Su acción prepara al organismo para la respuesta de “lucha o huida”, favoreciendo la acción rápida y eficiente ante estímulos demandantes.

# Sistema Nervioso Parasimpático (SNP)
Predomina en estados de reposo. Sus efectos sobre el corazón son:

-Disminución de la frecuencia cardíaca (bradicardia).
-Aumento de la variabilidad de la frecuencia cardíaca.
-Regulación mediante el nervio vago.
-Se relaciona con procesos de descanso, recuperación y equilibrio fisiológico.
El balance simpático-parasimpático se refleja directamente en la dinámica de los intervalos entre latidos, lo cual puede medirse y analizarse a través de la HRV.

 # Señal Electrocardiográfica (ECG) y Picos R

 <img width="1600" height="1253" alt="image" src="https://github.com/user-attachments/assets/eed7422a-1ccb-4a6e-b621-175a0c657aee" />


El ECG registra la actividad eléctrica del corazón mediante electrodos superficiales.
El complejo QRS representa la despolarización ventricular, y dentro de él, el pico R es el punto de mayor amplitud.
La detección de estos picos permite calcular los intervalos R-R, es decir, el tiempo entre latidos consecutivos. Esta serie temporal constituye el insumo principal para el análisis de la HRV.

 # Variabilidad de la Frecuencia Cardíaca (HRV)

 <img width="4166" height="1944" alt="image" src="https://github.com/user-attachments/assets/e427f3a8-ae78-4977-9031-4ce1e530c8c4" />


La HRV se define como la fluctuación natural de los intervalos R-R a lo largo del tiempo. Estas variaciones reflejan cómo el SNA modula la actividad del corazón ante estímulos internos y externos.

Una HRV alta suele indicar mayor actividad parasimpática y mejor capacidad de adaptación fisiológica.
Una HRV baja se asocia con predominio simpático, estrés, fatiga o condiciones patológicas.

# Análisis en el dominio del tiempo

Los indicadores más comunes son:

-Media de los intervalos R-R
-Representa el promedio del tiempo entre latidos. Una media mayor tiende a relacionarse con una frecuencia cardíaca más baja y mayor actividad vagal.
SDNN (Standard Deviation of NN intervals)
Es la desviación estándar de los intervalos R-R. Refleja la variabilidad global y es un indicador importante de la modulación autonómica.
Estos parámetros permiten comparar estados fisiológicos diferentes, como el reposo versus la lectura en voz alta evaluada en este laboratorio.

# Procesamiento Digital aplicado a la señal ECG

## Filtrado Digital e IIR

Las señales ECG contienen ruido de múltiples fuentes: interferencia de red, artefactos musculares, ruido de electrodos y deriva de línea base. Por ello es necesario aplicar filtros digitales antes del análisis.

Los filtros IIR (Infinite Impulse Response) son ampliamente utilizados por su eficiencia computacional. Un filtro IIR cumple una ecuación en diferencias donde el valor actual de la salida depende tanto de entradas presentes/pasadas como de salidas anteriores.
Su diseño implica definir:
Frecuencias de corte,Orden del filtro,tipo de aproximación (Butterworth, Chebyshev, etc.).
La correcta elección del filtro garantiza que la señal ECG conserve la morfología necesaria para detectar con precisión los picos R.

# Diagrama de Poincaré

<img width="569" height="595" alt="image" src="https://github.com/user-attachments/assets/035b3412-029b-4f67-bf64-7f639b3b3538" />


El diagrama de Poincaré es una herramienta gráfica utilizada para estudiar la dinámica de la serie de intervalos R-R. Consiste en representar cada intervalo 
𝑅𝑅𝑛 frente al siguiente 𝑅𝑅𝑛+1RRn+1
La forma y dispersión de la nube de puntos permiten identificar patrones de variabilidad cardíaca:
Mayor dispersión - mayor variabilidad - mayor influencia parasimpática.
Puntos concentrados - menor variabilidad - predominio simpático.
A partir del diagrama se pueden obtener índices relevantes:

# CVI (Cardiac Vagal Index)

Relaciona la dispersión perpendicular a la línea de identidad. Un CVI mayor indica mayor actividad parasimpática.

# CSI (Cardiac Sympathetic Index)

Relaciona la dispersión a lo largo de la línea de identidad. Valores altos están asociados con mayor actividad simpática.

Estos índices son especialmente útiles para comparar respuestas autonómicas en diferentes tareas, como el reposo frente a la verbalización.

# Procedimiento analisis y resultados:

## PARTE A. 
### a. Fundamento teórico 
Antes de iniciar la práctica, los estudiantes deberán realizar una investigación 
teórica que incluya los siguientes temas:  - - - - 
Actividad simpática y parasimpática del sistema nervioso autónomo, 
Efecto de la actividad simpática y parasimpática en la frecuencia 
cardíaca, 
Variabilidad de la frecuencia cardíaca (HRV) obtenida a partir de la señal 
electrocardiográfica (ECG), 
Diagrama de Poincaré como herramienta de análisis de la serie R-R. 
## b. Adquisición de la señal ECG  
Seleccionar a un sujeto de prueba para adquirir la señal electrocardiográfica; 
grabar la señal ECG durante 4 minutos, de los cuales, el participante 
permanecerá inmóvil y en silencio total durante los 2 primeros minutos, y 
luego leerá en voz alta un pasaje de un texto seleccionado por el equipo 
durante los dos últimos minutos. 
Verificar que la frecuencia de muestreo y los niveles de cuantificación 
establecidos sean los apropiados para este tipo de señal. 

```python  
import numpy as np
import matplotlib.pyplot as plt

# Cargar señal ECG desde Drive
from google.colab import drive
drive.mount('/content/drive')

# Ruta del archivo
ruta = '/content/lab 5 senal.txt'

# Cargar datos
data = np.loadtxt(ruta)    # <--- ESTA LÍNEA FALTABA
ecg = data[:, 1]           # segunda columna

# Frecuencia de muestreo
fs = 1000  # Hz

# Crear vector de tiempo
t = np.arange(len(ecg)) / fs

# Graficar un segmento

inicio = 0        # en segundos
duracion = 4      # segundos
m1 = int(inicio * fs)
m2 = int((inicio + duracion) * fs)

plt.figure(figsize=(14,4))
plt.plot(t[m1:m2], ecg[m1:m2], linewidth=0.8, color="red")
plt.title(f"Segmento del ECG ({inicio}s a {inicio+duracion}s)")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (mV)")
plt.grid(True)
plt.tight_layout()
plt.show()
```


<img width="1389" height="390" alt="image" src="https://github.com/user-attachments/assets/7e1532b4-946b-4510-a43f-ec0b71fc3638" />


## PARTE B 
b. Adquisición de la señal ECG
La señal electrocardiográfica (ECG) utilizada en este proyecto fue adquirida siguiendo el protocolo establecido en la guía de práctica. Se seleccionó un sujeto de prueba y se realizó un registro de 4 minutos, dividido en dos fases:
Fase 1: Reposo (0–2 min)
El participante permaneció inmóvil, en silencio y en condición basal para registrar la actividad cardíaca sin estímulos externos.
Fase 2: Lectura en voz alta (2–4 min)
El participante leyó un fragmento de texto seleccionado, con el fin de inducir cambios fisiológicos asociados al esfuerzo cognitivo y la modulación autonómica.
La frecuencia de muestreo de 1000 Hz garantiza una resolución temporal suficiente para detectar los picos R con precisión y permite el análisis de HRV sin distorsiones.
### Diseño del filtro
Este filtro se diseñó e implementó como un filtro IIR ( infinite impulse response) qué se relaciona con el Butter World en configuración pasa banda. Nuestra elección del Butterworth es debido a su respuesta en frecuencia plana en la banda. De paso, qué minimiza la distorsión de la onda QRS, que para nosotros como futuros ingenieros biomédicos es vital.
filto digital butterword
def design_bandpass_butter(lowcut, highcut, fs, order=4):

```python  
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter, find_peaks

# Cargar la señal (segunda columna del .txt)

ruta = '/content/lab 5 senal.txt'

data = np.loadtxt(ruta)
ecg = data[:, 1]          # la segunda columna
fs = 1000.0               # Hz (frecuencia de muestreo)

t = np.arange(len(ecg)) / fs

print("Forma de la señal:", ecg.shape)
print("Duración total (s):", len(ecg)/fs)

# Diseño del filtro IIR (Butterworth pasa banda 0.5–40 Hz)

lowcut = 0.5   # Hz
highcut = 40.0 # Hz
order = 4      # orden del filtro IIR

nyq = fs / 2.0
low = lowcut / nyq
high = highcut / nyq

b, a = butter(order, [low, high], btype='bandpass')

print("Coeficientes b:", b)
print("Coeficientes a:", a)

# --- Ecuación en diferencias (forma general) -----------------
# y[n] = -a[1]*y[n-1] - a[2]*y[n-2] - ... - a[order]*y[n-order]
#        + b[0]*x[n] + b[1]*x[n-1] + ... + b[order]*x[n-order]
# (con condiciones iniciales y[n<0] = 0, x[n<0] = 0)

#  Implementar el filtro (condiciones iniciales en 0)

ecg_filt = lfilter(b, a, ecg)   # lfilter asume condiciones iniciales en 0

# Comparar un segmento antes / después del filtrado
inicio = 0       # s
duracion = 4     # s
m1 = int(inicio * fs)
m2 = int((inicio + duracion) * fs)

plt.figure(figsize=(14,4))
plt.plot(t[m1:m2], ecg[m1:m2], label="ECG original", alpha=0.5)
plt.plot(t[m1:m2], ecg_filt[m1:m2], label="ECG filtrada", linewidth=1)
plt.title("Segmento de ECG (antes y después del filtrado)")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (mV)")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Dividir la señal filtrada en 2 segmentos de 2 min

dur_seg = 120  # segundos (2 minutos)
N_seg = int(dur_seg * fs)

seg1 = ecg_filt[0:N_seg]
seg2 = ecg_filt[N_seg:2*N_seg]

t1 = np.arange(len(seg1)) / fs
t2 = np.arange(len(seg2)) / fs

print("Muestras por segmento:", N_seg)

# Detección de picos R en cada segmento

# Parámetros básicos para find_peaks
dist_min = int(0.3 * fs)  # al menos 300 ms entre latidos
thr1 = np.mean(seg1) + 0.5*np.std(seg1)
thr2 = np.mean(seg2) + 0.5*np.std(seg2)

peaks1, _ = find_peaks(seg1, distance=dist_min, height=thr1)
peaks2, _ = find_peaks(seg2, distance=dist_min, height=thr2)

print("Nº de picos R en segmento 1:", len(peaks1))
print("Nº de picos R en segmento 2:", len(peaks2))

# Graficar picos R en cada segmento
plt.figure(figsize=(14,4))
plt.plot(t1, seg1, label="Segmento 1 filtrado")
plt.plot(t1[peaks1], seg1[peaks1], "ro", label="Picos R")
plt.title("Picos R - Segmento 1 (0–2 min)")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (mV)")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

plt.figure(figsize=(14,4))
plt.plot(t2, seg2, label="Segmento 2 filtrado")
plt.plot(t2[peaks2], seg2[peaks2], "ro", label="Picos R")
plt.title("Picos R - Segmento 2 (2–4 min)")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (mV)")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Intervalos R-R en segundos
rr1 = np.diff(peaks1) / fs
rr2 = np.diff(peaks2) / fs

# Tiempo asociado a cada RR (tomar el punto medio entre dos R)
t_rr1 = t1[peaks1[1:]]   # o (t1[peaks1[1:]] + t1[peaks1[:-1]])/2
t_rr2 = t2[peaks2[1:]]

print("RR segmento 1 (s):", rr1[:10])
print("RR segmento 2 (s):", rr2[:10])

# Graficar nueva señal: serie R-R
plt.figure(figsize=(10,4))
plt.plot(t_rr1, rr1, "-o")
plt.title("Nueva señal: intervalos R-R (Segmento 1)")
plt.xlabel("Tiempo (s)")
plt.ylabel("RR (s)")
plt.grid(True)
plt.tight_layout()
plt.show()

plt.figure(figsize=(10,4))
plt.plot(t_rr2, rr2, "-o")
plt.title("Nueva señal: intervalos R-R (Segmento 2)")
plt.xlabel("Tiempo (s)")
plt.ylabel("RR (s)")
plt.grid(True)
plt.tight_layout()
plt.show()

```


Nuestra frecuencia de muestreo fue de 1000 Hertz, las frecuencias de corte fueron de 0.5 Hz a 40 Hz.

El orden del filtro fue de orden cuatro para la función de transferencia que se dio en el diseño, ya que este es un filtro, pasa banda, quiere decir que es un filtro IIR de octavo orden, porque hay cuatro polos para el corte bajo y cuatro para el corte alto lo que nos da una atenuación lo suficientemente amplia en la rechaza banda sin introducir una complejidad computacional.

Implementación y ecuación en diferencias
El filtro se implementó a través de su ecuación de diferencias, utilizando los coeficientes normalizados B, del numerador y A, del denominador que se obtuvieron en el diseño. A continuación, la ecuación fundamental.

<img width="337" height="80" alt="image" src="https://github.com/user-attachments/assets/219b6d39-fdaf-4c9e-872c-95aa5f70a441" />

En esta ecuación x[n] es la señal de entrada y y[n] es la es la señal ya filtrada. En la programación, la implementación con la función ‘lfilter’ asumir la señal en reposo, estableciendo las condiciones iniciales en cero tal como nos lo indica la guía. Como resultado, tenemos la gráfica del segmento electrocardiográfica filtrado que nos demuestra un excelente atenuación del ruido de la línea base y una alta definición de los picos R, lo que rectifica el funcionamiento del diseño del filtro IIR.

Detección de picos R y generación de la serie RR.
La señal filtrada que es aproximadamente de unos 244.35 segundos de duración, se segmentó en dos bloques de 120 segundos o dos minutos para permitir un análisis comparativo de la HR V. A lo largo del tiempo.


<img width="1032" height="395" alt="image" src="https://github.com/user-attachments/assets/d858eb83-bca3-4d33-84f4-af69a2fee074" />


Para la detección de los picos RS empleó la función de ‘find_peaks’ , la distancia mínima fue de 0.3 segundos y este valor evita la detección de artefactos que no son correspondientes a la onda QRS, como si fueran latidos independientes porque un corazón humano no puede tirar frecuencia superiores a los 3.33 latidos por segundo o 200 latidos por minuto de forma sostenida, se utilizó un umbral dinámico, basado en las estadísticas de los segmentos, en donde se adaptaron las variaciones de la amplitud y el ruido residual.

En el primer segmento de cero a dos minutos se detectaron 196 picos R. Y en el segundo segmento de dos a cuatro minutos se detectaron 207 picos R.

Los tiempos de ocurrencia de los picos se utilizaron para calcular la serie de intervalos RR, este intervalo se calcula como la diferencia de tiempo entre los dos picos R sucesivos.


<img width="1041" height="678" alt="image" src="https://github.com/user-attachments/assets/03261957-1d2f-44bf-8402-53f8fb2c8d6f" />


<img width="1109" height="777" alt="image" src="https://github.com/user-attachments/assets/b28cd08d-fe71-495b-af5d-a6604fded714" />



## PARTE C 
e. Construcción del diagrama de Poincaré 
Obtener el diagrama de Poincaré para cada segmento de señal ECG y 
comparar la dispersión de la nube de puntos que se obtuvo para cada caso.   
Calcular los valores de los índices tanto de actividad vagal (CVI) como de 
actividad simpática (CSI) que se obtienen a partir del diagrama de Poincaré. 


## Diagramas de flujo
### Parte A:


<img width="297" height="663" alt="image" src="https://github.com/user-attachments/assets/7da46bce-8784-4032-ac08-c03289793cae" />



## Conclusiones


## Bibliografia
