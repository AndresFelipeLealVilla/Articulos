# Dataset crudo: V-Dem CY-Full+Others v16

Este archivo no está incluido en el repositorio porque excede el límite de
100MB de GitHub (pesa más de 300MB). Además, no tiene sentido alojar una
copia propia de un dataset público que la fuente original ya distribuye
libremente.

## Cómo obtenerlo

1. Ve a https://www.v-dem.net/data/the-v-dem-dataset/
2. Descarga la versión **"Country-Year: V-Dem Full+Others"**, versión **v16**
   (la misma versión usada en este análisis; versiones posteriores pueden
   tener columnas o codificaciones distintas).
3. Guarda el archivo descargado como `V-Dem-CY-Full_Others-v16.csv` en esta
   misma carpeta (`data/raw/`) si vas a ejecutar el cuaderno
   `01_limpieza_de_datos.ipynb` localmente.

## Nota sobre reproducibilidad

El archivo procesado y ya reducido a las variables de este proyecto
(`data/processed/vdem_exclusion_subset.csv`) sí está incluido en el
repositorio, y es suficiente para reproducir todos los cuadernos del
02 en adelante sin necesidad de descargar el dataset completo.
