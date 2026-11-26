# Datasets para cursos UNAM

Repositorio de datasets utilizados en mis cursos de la Facultad de Ingeniería, UNAM.

**Autor:** Miguel Serrano Reyes — Departamento de Ingeniería en Sistemas Biomédicos.

---

## Contenido

| Archivo | Señal | fs | Duración | Muestras | Formato | Origen |
|---|---|---|---|---|---|---|
| `biosenales/ppg_dedo_15s.csv` | Fotopletismografía | 100 Hz | 15 s | 1 500 | CSV | Sintética |
| `biosenales/pcg_pulmonar_6s.wav` | Fonocardiograma | 4 000 Hz | 6 s | 24 000 | WAV | CirCor DigiScope |
| `biosenales/ecg_derivacion2_30s.csv` | Electrocardiograma | 250 Hz | 30 s | 7 500 | CSV | Fantasia Database |
| `biosenales/ecg_ambulatorio_60s.npz` | Electrocardiograma | 360 Hz | 60 s | 21 600 | NPZ | *(ver nota)* |
| `biosenales/eeg_erp_kramer_1000trials.npz` | Electroencefalograma, 2 × 1 000 ensayos | 500 Hz | 1 s por ensayo | 500 por ensayo | NPZ | Kramer & Eden |
| `biosenales/eeg_espectro_kramer_2s.npz` | Electroencefalograma, un canal | 1 000 Hz | 2 s | 2 000 | NPZ | Kramer & Eden |
| `biosenales/ecog_cortical_1s.npz` | Electrocorticograma, un electrodo | 500 Hz | 1 s | 500 | NPZ | Kramer & Eden |
| `biosenales/ecog_cortical_20s.npz` | Electrocorticograma, registro extendido | 500 Hz | 20 s | 10 000 | NPZ | Sintética |
| `biosenales/ecog_dos_electrodos_100ensayos.npz` | Electrocorticograma, 2 electrodos × 100 ensayos | 500 Hz | 1 s por ensayo | 500 por ensayo | NPZ | Kramer & Eden |
| `biosenales/emg_biceps_15s.npz` | Electromiografía de superficie | 1 000 Hz | 15 s | 15 000 | NPZ | Sintética |
| `biosenales/eeg_erp_contaminado_10ensayos.npz` | Electroencefalograma, 10 ensayos con artefactos | 1 000 Hz | 1 s por ensayo | 1 000 por ensayo | NPZ | Kramer & Eden |

### Qué metadatos conserva cada formato

| Formato | Guarda la señal | Guarda la frecuencia de muestreo | Guarda otros metadatos |
|---|---|---|---|
| CSV | sí | **no** | no |
| WAV | sí | sí, en el encabezado | no |
| NPZ | sí | sí | sí, los que se quiera |

Al usar los archivos CSV, la frecuencia de muestreo debe suministrarse por separado.

El formato NPZ admite además **arreglos multidimensionales**, lo que permite almacenar
señales organizadas como matrices de ensayos, algo que ni CSV ni WAV pueden hacer.

---

## Procedencia y licencias

### `biosenales/ppg_dedo_15s.csv`

Señal de fotopletismografía (PPG) de dedo. **Generada sintéticamente**, con morfología
fisiológicamente plausible: pico sistólico, muesca dícrota, pico diastólico secundario,
modulación respiratoria, variabilidad de la frecuencia cardíaca, ruido de banda ancha
de bajo nivel y un artefacto de movimiento alrededor de t = 10.1 s.

Frecuencia cardíaca media: 72 lpm. Amplitud en unidades arbitrarias.

| Columna | Contenido |
|---|---|
| `muestra` | índice entero, de 0 a 1499 |
| `amplitud` | valor de la señal en unidades arbitrarias |

El archivo **no contiene la frecuencia de muestreo**; debe suministrarse por separado
(fs = 100 Hz).

**Licencia:** libre uso con atribución.

---

### `biosenales/pcg_pulmonar_6s.wav`

Fonocardiograma registrado en el foco pulmonar (6 s, fs = 4000 Hz, PCM 16 bits, mono).
Fragmento de 0.75 s a 6.75 s extraído del registro `85217_PV.wav`, correspondiente a un
sujeto adolescente sin soplos. Frecuencia cardíaca media: 74 lpm.

El formato WAV almacena la frecuencia de muestreo en su encabezado, por lo que
`scipy.io.wavfile.read` la devuelve junto con los datos.

Oliveira, J., Renna, F., Costa, P., Nogueira, M., Oliveira, A. C., Elola, A., Ferreira, C.,
Jorge, A., Bahrami Rad, A., Reyna, M., Sameni, R., Clifford, G., & Coimbra, M. (2022).
*The CirCor DigiScope Phonocardiogram Dataset* (version 1.0.1). PhysioNet.
https://doi.org/10.13026/7bkn-d780

Publicación original: J. H. Oliveira et al. (2021). *The CirCor DigiScope Dataset: From
Murmur Detection to Murmur Classification.* IEEE Journal of Biomedical and Health
Informatics. https://doi.org/10.1109/JBHI.2021.3137048

**Licencia:** Open Data Commons Attribution License v1.0

---

### `biosenales/ecg_derivacion2_30s.csv`

Electrocardiograma de superficie (30 s, fs = 250 Hz, 7 500 muestras, mV).
Fragmento de los segundos 616 a 646 del registro `f1y03`, correspondiente a un sujeto
joven sano en reposo supino y ritmo sinusal. Frecuencia cardíaca media 66 lpm.

Características relevantes para uso docente: componente de directa de aproximadamente
8.15 mV, tendencia lineal de −0.0088 mV/s, y una excursión de línea base de 1.4 mV
alrededor de t = 10 s que no es de forma lineal.

| Columna | Contenido |
|---|---|
| `muestra` | índice entero, de 0 a 7499 |
| `amplitud_mV` | amplitud en milivoltios |

El archivo **no contiene la frecuencia de muestreo**; debe suministrarse por separado
(fs = 250 Hz).

Iyengar N, Peng C-K, Morin R, Goldberger AL, Lipsitz LA. *Age-related alterations in the
fractal scaling of cardiac interbeat interval dynamics.* Am J Physiol 1996;271:1078-1084.

Goldberger AL, Amaral LAN, Glass L, Hausdorff JM, Ivanov PCh, Mark RG, Mietus JE,
Moody GB, Peng C-K, Stanley HE. *PhysioBank, PhysioToolkit, and PhysioNet.*
Circulation 101(23):e215-e220, 2000.

Base de datos: Fantasia Database v1.0.0, PhysioNet. https://doi.org/10.13026/C24G6C

---

### `biosenales/ecg_ambulatorio_60s.npz`

Electrocardiograma de superficie (60 s, fs = 360 Hz, 21 600 muestras).
Frecuencia cardíaca media 74 lpm, variabilidad del intervalo RR de 4.6 %.
Morfología P-QRS-T bien definida y línea base estable.

Convertido desde un archivo `.mat` original. La señal se almacenó digitalizada con una
ganancia de 200 unidades ADC por milivoltio; el archivo conserva tanto los datos crudos
como la versión convertida a mV.

| Clave | Contenido |
|---|---|
| `ecg_mV` | señal en milivoltios, `float32` |
| `val_adc` | datos crudos del convertidor, `int16` |
| `fs_Hz` | 360 |
| `ganancia_adu_por_mV` | 200 |
| `unidades` | `'mV'` |
| `n_muestras` | 21600 |
| `duracion_s` | 60.0 |
| `descripcion` | cadena descriptiva |

Lectura:

```python
import numpy as np
d   = np.load('ecg_ambulatorio_60s.npz')
ecg = d['ecg_mV']
Fs  = int(d['fs_Hz'])
```

> **PENDIENTE — completar la procedencia.** Los parámetros de este registro
> (fs = 360 Hz, ganancia 200 unidades por mV) corresponden a los de la MIT-BIH
> Arrhythmia Database de PhysioNet, pero el origen exacto no está confirmado.
> Antes de considerar este archivo redistribuible, verificar la base y el número de
> registro de los que proviene, y añadir aquí la cita y la licencia correspondientes.

---

### `biosenales/eeg_erp_kramer_1000trials.npz`

EEG de cuero cabelludo registrado con un solo electrodo durante una tarea auditiva
de dos condiciones. Mil ensayos por condición, 1 s por ensayo, fs = 500 Hz,
estímulo presentado a t = 0.25 s. Amplitud en microvoltios.

A diferencia de los demás archivos del repositorio, este contiene señales organizadas
como **matrices de ensayos**: cada fila es una repetición del experimento y cada
columna un instante de tiempo.

| Clave | Contenido |
|---|---|
| `EEGa` | condición A (tono agudo), matriz 1000 × 500, `float64` |
| `EEGb` | condición B (tono grave), matriz 1000 × 500, `float64` |
| `t` | vector temporal de 500 muestras, en segundos |
| `fs_Hz` | 500 |
| `t_estimulo_s` | 0.25 |
| `unidades` | `'microvoltios'` |
| `n_trials` | 1000 |
| `n_muestras` | 500 |
| `descripcion` | cadena descriptiva |

Lectura:

```python
import numpy as np
d    = np.load('eeg_erp_kramer_1000trials.npz')
EEGa = d['EEGa']          # (1000, 500)
EEGb = d['EEGb']          # (1000, 500)
t    = d['t']             # (500,)
Fs   = int(d['fs_Hz'])    # 500
```

Convertido desde `02_EEG-1.mat` sin modificar los datos; se verificó que los valores
son idénticos al original y que el estadístico max |ERP_A − ERP_B| = 0.2884 coincide
con el reportado en el libro.

Kramer, M. A., & Eden, U. T. *Case Studies in Neural Data Analysis: A Guide for the
Practicing Neuroscientist.* MIT Press, 2016. Capítulo 2, The Event-Related Potential.

Versión en Python: https://mark-kramer.github.io/Case-Studies-Python/02.html

---

### `biosenales/eeg_espectro_kramer_2s.npz`

EEG de cuero cabelludo registrado con un solo canal durante 2 s a 1 000 Hz.
Corresponde a un paciente inconsciente a quien se solicitó el estudio para
caracterizar su actividad cerebral. Amplitud en microvoltios.

Características relevantes para uso docente:

| Característica | Valor |
|---|---|
| Frecuencia de Nyquist | 500 Hz |
| Resolución espectral | 0.5 Hz |
| Componente dominante | 60.00 Hz, con casi 600 veces la potencia de cualquier componente cerebral |
| Contenido cerebral | predominio theta (≈ 6 Hz) en la primera mitad, alfa (≈ 11 Hz) en la segunda |

El registro contiene una componente muy estrecha y estable en 60 Hz, compatible con
interferencia de la red eléctrica. Su magnitud oculta por completo la actividad cerebral
si el espectro se grafica en escala lineal.

| Clave | Contenido |
|---|---|
| `eeg` | señal de 2 000 muestras, `float64` |
| `t` | vector temporal de 2 000 muestras, en segundos |
| `fs_Hz` | 1000 |
| `unidades` | `'microvoltios'` |
| `n_muestras` | 2000 |
| `duracion_s` | 2.0 |
| `descripcion` | cadena descriptiva |

Lectura:

```python
import numpy as np
d   = np.load('eeg_espectro_kramer_2s.npz')
eeg = d['eeg']            # (2000,)
t   = d['t']              # (2000,)
Fs  = int(d['fs_Hz'])     # 1000
```

Convertido desde `03_EEG-1.mat` sin modificar los datos; se verificó que los valores
son idénticos al original.

Kramer, M. A., & Eden, U. T. *Case Studies in Neural Data Analysis: A Guide for the
Practicing Neuroscientist.* MIT Press, 2016. Capítulo 3, The Power Spectrum (Part 1).

Versión en Python: https://mark-kramer.github.io/Case-Studies-Python/03.html

---

### `biosenales/ecog_cortical_1s.npz`

Electrocorticograma registrado con un electrodo implantado directamente sobre la corteza,
en una paciente con epilepsia bajo monitoreo invasivo. Un segundo a 500 Hz, en milivoltios.

| Característica | Valor |
|---|---|
| Frecuencia de Nyquist | 250 Hz |
| Resolución espectral | 1.0 Hz |
| Ritmo dominante | 6.0 Hz |
| Rango | −14.4 a +18.8 mV |

Al durar un solo segundo, su resolución espectral es limitada y no admite promediado por
segmentos. Es útil para estudiar fuga espectral y el efecto de las ventanas, no para
métodos de estimación que requieren promediar.

| Clave | Contenido |
|---|---|
| `ecog` | señal de 500 muestras, `float64` |
| `t` | vector temporal, en segundos |
| `fs_Hz` | 500 |
| `unidades` | `'mV'` |
| `n_muestras` | 500 |
| `duracion_s` | 1.0 |
| `descripcion` | cadena descriptiva |

Convertido desde `04_ECoG-1.mat` sin modificar los datos; se verificó que los valores son
idénticos al original.

Kramer, M. A., & Eden, U. T. *Case Studies in Neural Data Analysis: A Guide for the
Practicing Neuroscientist.* MIT Press, 2016. Capítulo 4, The Power Spectrum (Part 2).

Versión en Python: https://mark-kramer.github.io/Case-Studies-Python/04.html

---

### `biosenales/ecog_cortical_20s.npz`

**Señal generada, no registrada.** Veinte segundos a 500 Hz, en milivoltios, construida
para docencia con la misma frecuencia de muestreo y escala de amplitud que el registro
anterior.

Se generó porque aquel dura un segundo, lo cual no permite ilustrar métodos de estimación
espectral que requieren promediar varios segmentos.

Composición:

| Componente | Frecuencia | Descripción |
|---|---|---|
| Fondo | — | ruido con espectro $1/f^2$ |
| Ritmo dominante | 6.3 Hz | banda estrecha, con amplitud modulada |
| Componente débil | 12.4 Hz | banda estrecha, 22 dB por debajo del dominante |
| Banda ancha | 21 Hz | ancho de banda de 4 Hz |

Las frecuencias de los ritmos **no coinciden con los bins** de la DFT para las duraciones
de segmento habituales, de modo que la fuga espectral resulta observable. El contenido por
encima de 20 Hz representa el 12.4 % de la potencia total, frente al 13.9 % del registro
real, y la pendiente del fondo entre 40 y 200 Hz es de −1.99.

| Clave | Contenido |
|---|---|
| `ecog` | señal de 10 000 muestras, `float64` |
| `t` | vector temporal, en segundos |
| `fs_Hz` | 500 |
| `unidades` | `'mV'` |
| `n_muestras` | 10000 |
| `duracion_s` | 20.0 |
| `semilla` | 20261023 |
| `componentes` | descripción de las componentes |
| `descripcion` | cadena descriptiva |

**Licencia:** libre uso con atribución.
---

### `biosenales/ecog_dos_electrodos_100ensayos.npz`

Electrocorticograma registrado **simultáneamente con dos electrodos corticales** en una
paciente bajo monitoreo invasivo, durante cien repeticiones de una misma tarea.
Cien ensayos de un segundo, fs = 500 Hz, en milivoltios.

Es el único archivo del repositorio con **dos señales registradas a la vez**, lo que
permite estudiar la relación entre ellas y no solo sus propiedades individuales.

Características relevantes para uso docente:

| Característica | Valor |
|---|---|
| Ritmo dominante en ambos electrodos | 8.0 Hz |
| Potencia en 8 Hz | 0.50 (la mayor del espectro) |
| **Coherencia en 8 Hz** | **0.14** |
| Potencia en 24 Hz | 0.00073, el 0.15 % de la de 8 Hz |
| **Coherencia en 24 Hz** | **0.77** |

Ese contraste es lo que hace valioso el registro: los dos electrodos oscilan con fuerza
a la misma frecuencia **sin mantener una relación de fase consistente**, mientras que una
componente mil veces más débil sí está acoplada. Medido sobre los cien ensayos, la
longitud del vector resultante de las diferencias de fase es 0.137 en 8 Hz y 0.856 en 24 Hz.

| Clave | Contenido |
|---|---|
| `E1` | electrodo 1, matriz 100 × 500, `float64` |
| `E2` | electrodo 2, matriz 100 × 500, `float64` |
| `t` | vector temporal de 500 muestras, en segundos |
| `fs_Hz` | 500 |
| `unidades` | `'mV'` |
| `n_ensayos` | 100 |
| `n_muestras` | 500 |
| `duracion_s` | 1.0 |
| `descripcion` | cadena descriptiva |

Lectura:

```python
import numpy as np
d  = np.load('ecog_dos_electrodos_100ensayos.npz')
E1 = d['E1']              # (100, 500)
E2 = d['E2']              # (100, 500)
t  = d['t']               # (500,)
Fs = int(d['fs_Hz'])      # 500
```

Convertido desde `ECoG-1.mat` sin modificar los datos; se verificó que los valores son
idénticos al original.

Kramer, M. A., & Eden, U. T. *Case Studies in Neural Data Analysis: A Guide for the
Practicing Neuroscientist.* MIT Press, 2016. Capítulo 5, Coherence.

Versión en Python: https://mark-kramer.github.io/Case-Studies-Python/05.html

---

### `biosenales/emg_biceps_15s.npz`

Electromiografía de superficie del bíceps braquial. Quince segundos a 1 000 Hz,
en milivoltios, con periodos de reposo y varias contracciones voluntarias de distinta
intensidad.

| Característica | Valor |
|---|---|
| Componente de directa | ≈ +0.043 mV |
| Desviación en reposo | ≈ 0.130 mV |
| Desviación en contracción | ≈ 0.418 mV |
| Contracciones claras | 4.6–6.4 s, 7.5–9.5 s, 12.6–14.0 s |
| Contracción débil | ≈ 11 s |

Reparto de la potencia: 3.6 % por debajo de 20 Hz, 24.5 % entre 20 y 150 Hz —la banda
asociada a la actividad muscular— y 72.0 % por encima de 150 Hz.

La contracción débil de los 11 segundos es útil para discutir la elección de un umbral
de detección: con un umbral bajo se detecta pero otras contracciones se fragmentan, y
con uno alto desaparece. No existe un valor que acierte en todos los casos.

| Clave | Contenido |
|---|---|
| `emg` | señal de 15 000 muestras, `float64` |
| `t` | vector temporal, en segundos |
| `fs_Hz` | 1000 |
| `unidades` | `'mV'` |
| `n_muestras` | 15000 |
| `duracion_s` | 15.0 |
| `descripcion` | cadena descriptiva |

**Licencia:** libre uso con atribución.

---

### `biosenales/eeg_erp_contaminado_10ensayos.npz`

Diez ensayos de EEG de un segundo cada uno, muestreados a 1 000 Hz, registrados durante
una tarea con estímulo repetido. En milivoltios.

El registro contiene un potencial evocado que **no es visible directamente**: queda
enmascarado por dos contaminaciones de naturaleza distinta.

| Característica | Valor |
|---|---|
| Interferencia de línea | 60.00 Hz, **86.8 %** de la potencia total |
| Artefacto transitorio | uno por ensayo, en instantes variables, de 7 a 9 mV |
| Banda fisiológica (5–30 Hz) | 1.5 % de la potencia |
| Potencial evocado | ≈ +0.32 mV alrededor de t = 0.51 s, visible tras filtrar |

Las dos contaminaciones piden estrategias opuestas: la interferencia ocupa una banda
propia y se puede filtrar, mientras que los artefactos transitorios no la tienen y
filtrarlos solo los esparce en el tiempo. Como ocurren en instantes distintos en cada
ensayo, el promediado los atenúa.

| Clave | Contenido |
|---|---|
| `eeg` | matriz de 10 × 1000, `float64` |
| `t` | vector temporal, en segundos |
| `fs_Hz` | 1000 |
| `unidades` | `'mV'` |
| `n_ensayos` | 10 |
| `n_muestras` | 1000 |
| `duracion_s` | 1.0 |
| `descripcion` | cadena descriptiva |

Convertido desde `EEG-1.mat` sin modificar los datos; se verificó que los valores son
idénticos al original.

Kramer, M. A., & Eden, U. T. *Case Studies in Neural Data Analysis: A Guide for the
Practicing Neuroscientist.* MIT Press, 2016. Capítulo 6, Filtering Field Data.

Versión en Python: https://mark-kramer.github.io/Case-Studies-Python/06.html

---

## Uso

Los archivos pueden descargarse directamente desde su URL cruda:

```
https://raw.githubusercontent.com/MiguelSerranoReyes/datasets/main/biosenales/NOMBRE_DEL_ARCHIVO
```

Ejemplo en Python:

```python
import urllib.request, os

URL = ('https://raw.githubusercontent.com/MiguelSerranoReyes/datasets/'
       'main/biosenales/eeg_espectro_kramer_2s.npz')
ARCHIVO = 'eeg_espectro_kramer_2s.npz'

if not os.path.exists(ARCHIVO):
    urllib.request.urlretrieve(URL, ARCHIVO)
```

---

## Convención de nombres

`tipoDeSeñal_sitioOCondición_duración.extensión`

Ejemplos: `ppg_dedo_15s.csv`, `pcg_pulmonar_6s.wav`, `ecg_derivacion2_30s.csv`,
`eeg_espectro_kramer_2s.npz`

Cuando el archivo contiene **matrices de ensayos** en lugar de una señal continua, el
último campo indica el número de ensayos en vez de la duración total:
`eeg_erp_contaminado_10ensayos.npz`, `ecog_dos_electrodos_100ensayos.npz`.
