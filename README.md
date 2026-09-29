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

### Qué metadatos conserva cada formato

| Formato | Guarda la señal | Guarda la frecuencia de muestreo | Guarda otros metadatos |
|---|---|---|---|
| CSV | sí | **no** | no |
| WAV | sí | sí, en el encabezado | no |
| NPZ | sí | sí | sí, los que se quiera |

Al usar los archivos CSV, la frecuencia de muestreo debe suministrarse por separado.

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

Contenido del archivo:

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
d = np.load('ecg_ambulatorio_60s.npz')
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

| Clave | Contenido |
|---|---|
| `EEGa` | condición A (tono agudo), matriz 1000 × 500 |
| `EEGb` | condición B (tono grave), matriz 1000 × 500 |
| `t` | vector temporal de 500 muestras, en segundos |
| `fs_Hz` | 500 |
| `t_estimulo_s` | 0.25 |
| `unidades` | `'microvoltios'` |

Convertido desde `02_EEG-1.mat`.

Kramer, M. A., & Eden, U. T. *Case Studies in Neural Data Analysis: A Guide for the
Practicing Neuroscientist.* MIT Press, 2016. Capítulo 2, The Event-Related Potential.

Versión en Python: https://mark-kramer.github.io/Case-Studies-Python/02.html

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
       'main/biosenales/ecg_ambulatorio_60s.npz')
ARCHIVO = 'ecg_ambulatorio_60s.npz'

if not os.path.exists(ARCHIVO):
    urllib.request.urlretrieve(URL, ARCHIVO)
```

---

## Convención de nombres

`tipoDeSeñal_sitioOCondición_duración.extensión`

Ejemplos: `ppg_dedo_15s.csv`, `pcg_pulmonar_6s.wav`, `ecg_derivacion2_30s.csv`