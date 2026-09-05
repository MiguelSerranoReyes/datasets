# Datasets para cursos UNAM

Repositorio de datasets utilizados en mis cursos de la Facultad de Ingeniería, UNAM.

**Autor:** Miguel Serrano Reyes — Departamento de Ingeniería en Sistemas Biomédicos.

---

## Contenido

| Archivo | Señal | fs | Duración | Muestras | Origen |
|---|---|---|---|---|---|
| `biosenales/ppg_dedo_15s.csv` | Fotopletismografía | 100 Hz | 15 s | 1500 | Sintética |
| `biosenales/pcg_pulmonar_6s.wav` | Fonocardiograma | 4000 Hz | 6 s | 24000 | CirCor DigiScope |

---

## Procedencia y licencias

### `biosenales/ppg_dedo_15s.csv`

Señal de fotopletismografía (PPG) de dedo. **Generada sintéticamente**, con morfología
fisiológicamente plausible: pico sistólico, muesca dícrota, pico diastólico secundario,
modulación respiratoria, variabilidad de la frecuencia cardíaca, ruido de banda ancha
de bajo nivel y un artefacto de movimiento alrededor de t = 10.1 s.

Frecuencia cardíaca media: 72 lpm. Amplitud en unidades arbitrarias.

Formato CSV con dos columnas:

| Columna | Contenido |
|---|---|
| `muestra` | índice entero, de 0 a 1499 |
| `amplitud` | valor de la señal en unidades arbitrarias |

El archivo **no contiene la frecuencia de muestreo**; debe suministrarse por separado
(fs = 100 Hz).

**Licencia:** libre uso con atribución.

### `biosenales/pcg_pulmonar_6s.wav`

Fonocardiograma registrado en el foco pulmonar (6 s, fs = 4000 Hz, PCM 16 bits, mono).
Fragmento de 0.75 s a 6.75 s extraído del registro `85217_PV.wav`, correspondiente a un
sujeto adolescente sin soplos. Frecuencia cardíaca media: 74 lpm.

Oliveira, J., Renna, F., Costa, P., Nogueira, M., Oliveira, A. C., Elola, A., Ferreira, C.,
Jorge, A., Bahrami Rad, A., Reyna, M., Sameni, R., Clifford, G., & Coimbra, M. (2022).
*The CirCor DigiScope Phonocardiogram Dataset* (version 1.0.1). PhysioNet.
https://doi.org/10.13026/7bkn-d780

Publicación original: J. H. Oliveira et al. (2021). *The CirCor DigiScope Dataset: From
Murmur Detection to Murmur Classification.* IEEE Journal of Biomedical and Health
Informatics. https://doi.org/10.1109/JBHI.2021.3137048

**Licencia:** Open Data Commons Attribution License v1.0

---

## Uso

Los archivos pueden descargarse directamente desde su URL cruda:

https://raw.githubusercontent.com/MiguelSerranoReyes/datasets/main/biosenales/NOMBRE_DEL_ARCHIVO

---

## Convención de nombres

`tipoDeSeñal_sitioOCondición_duración.extensión`

Ejemplos: `ppg_dedo_15s.csv`, `pcg_pulmonar_6s.wav`