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
## PARTE B 
b. Adquisición de la señal ECG
La señal electrocardiográfica (ECG) utilizada en este proyecto fue adquirida siguiendo el protocolo establecido en la guía de práctica. Se seleccionó un sujeto de prueba y se realizó un registro de 4 minutos, dividido en dos fases:
Fase 1: Reposo (0–2 min)
El participante permaneció inmóvil, en silencio y en condición basal para registrar la actividad cardíaca sin estímulos externos.
Fase 2: Lectura en voz alta (2–4 min)
El participante leyó un fragmento de texto seleccionado, con el fin de inducir cambios fisiológicos asociados al esfuerzo cognitivo y la modulación autonómica.
La frecuencia de muestreo de 1000 Hz garantiza una resolución temporal suficiente para detectar los picos R con precisión y permite el análisis de HRV sin distorsiones.
Diseño de filtro IIR con los parametros de la señal
codigo de python 
filto digital butterword
def design_bandpass_butter(lowcut, highcut, fs, order=4):

```python  
    nyq = 0.5 * fs
    if lowcut <= 0:
        low = 0.0001
    else:
        low = lowcut / nyq
    high = min(highcut / nyq, 0.999)
    if low >= high:
        raise ValueError("Frecuencias de corte inválidas para el fs dado.")
    b, a = butter(order, [low, high], btype='band')
    return b, a

def apply_filter(b, a, signal):
    return filtfilt(b, a, signal)
```



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
