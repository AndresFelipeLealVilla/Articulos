# Bolivia vs. Kosovo: exclusión política y ciencia de datos

Código y datos que sostienen el artículo ["Lo que los datos no ven: Caminos opuestos, resultados afines en Bolivia y Kosovo"](https://www.linkedin.com/pulse/lo-que-los-datos-ven-caminos-opuestos-resultados-en-y-leal-villa-oawxe/), publicado en LinkedIn.

El proyecto analiza patrones de exclusión política por grupo social, género y otras dimensiones de identidad en 179 países (2000-2023), usando datos de V-Dem, y desarrolla en profundidad el caso comparado de Bolivia y Kosovo.

## Fuente de datos

[V-Dem (Varieties of Democracy)](https://www.v-dem.net/), versión CY-Full+Others v16. V-Dem codifica variables de democracia y derechos políticos a partir de paneles de expertos país por país, no de encuestas a la población.

## Estructura del repositorio

```
notebooks/
├── 01_limpieza_de_datos.ipynb          Extracción y limpieza del subconjunto de variables de exclusión
├── 02_analisis_exclusion_social.ipynb   Estadística descriptiva y exploratoria, todos los países
├── 03_panel_efectos_fijos.ipynb         Regresión con efectos fijos de país y año
├── 04_causalidad_rezagada.ipynb         Precedencia estadística entre dimensiones de exclusión
├── 05_seleccion_de_paises.ipynb         Identificación de países atípicos/convergentes (residuales, trayectorias)
└── 06_comparacion_entre_paises.ipynb    Comparador Bolivia-Kosovo, gráficas y tabla final

data/
├── raw/          Dataset original de V-Dem, sin modificar
└── processed/    Subconjunto limpio de variables usado en el análisis (vdem_exclusion_subset.csv)
```

## Cómo reproducir el análisis

Los cuadernos están numerados en el orden en que deben ejecutarse. Requieren Python 3 y las siguientes librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`, `statsmodels`, `linearmodels`, `scikit-learn`, `tslearn`. Diseñados para correr en Google Colab; cada cuaderno carga el CSV correspondiente desde `/content/`, así que si los ejecutas localmente ajusta esas rutas a `data/processed/` o `data/raw/` según corresponda.

## Limitaciones metodológicas

Este proyecto documenta explícitamente los límites de cada técnica usada (regresión de residuales, panel de efectos fijos, clustering de trayectorias, precedencia rezagada) dentro de cada cuaderno y en el anexo metodológico del artículo. En resumen: V-Dem mide percepción experta, no experiencia vivida reportada; los controles de cada modelo son decisiones del autor, no especificaciones neutrales; y la selección de países para el estudio de caso, aunque partió de criterios estadísticos, está sujeta al sesgo de qué países tienen documentación periodística verificable disponible.

## Licencia y uso

Código disponible para revisión, réplica y reutilización. Los datos de V-Dem se rigen por los [términos de uso de V-Dem](https://www.v-dem.net/data/terms-of-use/); cítalos a ellos, no a este repositorio, si usas el dataset original.

## Autor

Andrés Felipe Leal Villa
