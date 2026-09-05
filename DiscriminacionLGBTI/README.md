# Lo que Colombia no investiga: auditoría de datos sobre homicidios de personas trans (2008-2025)

Análisis estadístico de 306 homicidios de personas trans documentados en Colombia, a partir del registro público de TGEU (*Transgender Europe*), contrastado con una fuente local independiente (Caribe Afirmativo) y sometido a pruebas de significancia para separar patrones reales de artefactos del método de recolección.

📄 **Artículo completo:** [`auditoria_violencia_trans_colombia.md`](./auditoria_violencia_trans_colombia.md)

---

## De qué trata esto

Este no es un perfil biográfico ni un recuento narrativo. Es una auditoría de datos que responde preguntas concretas con evidencia estadística, no con impresión:

- ¿Está aumentando la violencia contra personas trans en Colombia, o solo mejoró el monitoreo?
- ¿Qué proporción de los casos tiene alguna respuesta institucional documentada?
- ¿Es cierto que las grandes ciudades investigan más que el resto del país? (Spoiler: no.)
- ¿Qué tan completo es el registro de TGEU frente a lo que documenta una organización local?

Cada hallazgo se presenta junto con su límite estadístico explícito. Cuando un resultado inicial no se sostuvo bajo escrutinio (el caso del confusor identidad/época en la sección 4 del artículo), se reporta como tal en lugar de presentarse como conclusión.

## Estructura del repositorio

```
.
├── README.md
├── auditoria_violencia_trans_colombia.md      # Artículo final
├── tgeu_colombia_limpio.csv                   # Dataset de trabajo (306 filas, 29 columnas)
├── 2_analisis_descriptivo.ipynb               # Estadística descriptiva y tendencia temporal
├── 3_respuesta_institucional.ipynb            # Clasificación e impunidad
├── 4_Metodos_estadisticos_colombia.ipynb      # Fisher, Poisson, regresiones logísticas
└── 5Triangulacion_caribe_afirmativo.ipynb     # Contraste con fuente local independiente
```

## Fuente de datos

- **Principal:** TGEU (Transgender Europe), proyecto [*Trans Murder Monitoring*](https://transrespect.org/en/trans-murder-monitoring/), filtrado a Colombia. Es un monitoreo hecho por una ONG a partir de reportes de prensa y organizaciones locales, **no un registro oficial del Estado colombiano**.
- **De contraste:** Corporación Caribe Afirmativo, informes *Incontables: sin registro, no hay memoria* (2024) y *Con permiso para despreciar* (2025), usados para validar qué tan completo es el registro de TGEU en el mismo país y período.

## Métodos utilizados

| Pregunta | Método | Cuaderno |
|---|---|---|
| ¿Aumenta la violencia documentada? | Regresión de Poisson | `2_analisis_descriptivo.ipynb`, `4_Metodos_estadisticos_colombia.ipynb` |
| ¿Qué proporción tiene respuesta institucional? | Clasificación de 3 niveles + corrección de sesgo de selección | `3_respuesta_institucional.ipynb` |
| ¿Las capitales investigan más? | Regresión logística (`hubo_accion ~ año + capital`) | `4_Metodos_estadisticos_colombia.ipynb` |
| ¿Travesti vs. mujer trans reciben trato distinto? | Prueba exacta de Fisher + control por año | `4_Metodos_estadisticos_colombia.ipynb` |
| ¿Qué tan completo es TGEU? | Comparación directa de conteos anuales contra fuente local | `5Triangulacion_caribe_afirmativo.ipynb` |

## Cómo reproducir

1. Cloná el repositorio y abrí cualquiera de los cuadernos en Jupyter, Colab o VS Code.
2. Todos los cuadernos leen directamente `tgeu_colombia_limpio.csv` desde la raíz del repositorio (o `/content/` si se corren en Colab).
3. Se ejecutan de forma independiente entre sí; no hay dependencias de orden entre cuadernos, salvo que todos parten del mismo CSV limpio.
4. Requiere `pandas`, `numpy`, `matplotlib`, `scipy` y `statsmodels`.

Cada número citado en el artículo tiene su celda de origen referenciada explícitamente en la sección de **Notas** del artículo (nota 1 a 17).

## Protocolo ético sobre nombres de víctimas

Los dos casos individuales mencionados en el artículo (Sara Millerey González y Karis Saldarriaga) se seleccionaron y redactaron bajo un protocolo estricto:

- Se nombra únicamente con el nombre y la identidad de género que la persona reivindicó en vida.
- **Nunca** se usa un nombre legal previo, incluso si aparece en alguna cobertura de prensa disponible.
- Solo se incluyen personas con cobertura periodística verificable que ya las identificó correctamente; ninguna identidad fue inferida ni confirmada por este proyecto de forma independiente.
- El dataset de trabajo (`tgeu_colombia_limpio.csv`) no contiene nombres propios de víctimas: **no es posible confirmar** si estos dos casos corresponden a filas específicas del archivo. Se presentan como casos documentados dentro del mismo país y período que cubre el análisis, no como filas identificadas del CSV.

## Limitaciones reconocidas

- **Subregistro no cuantificable con precisión:** TGEU capta en promedio 54,5% de lo que documenta la fuente local comparable (2023-2024). No hay garantía de que ese factor sea constante en otros años o regiones.
- **Sesgo de selección en la variable de respuesta institucional:** solo se conoce el desenlace de un caso cuando hubo desenlace que reportar, lo que infla artificialmente la tasa de "éxito" entre los casos con desenlace conocido.
- **Confusor sin resolver:** el modelo que intenta separar el efecto de la identidad "travesti" del efecto del año de ocurrencia presenta cuasi-separación estadística perfecta y no converge. No se fuerza una conclusión con técnicas alternativas (por ejemplo, penalización de Firth); se reporta como pregunta abierta.
- **Sin denominador poblacional:** no existe un censo confiable del tamaño de la población trans en Colombia, por lo que no es posible convertir los conteos en una tasa por habitante.
- **Hallazgo de capitales sin mecanismo causal confirmado:** es una asociación estadística robusta, no una explicación. Se documentan tres hipótesis alternativas sin evidencia suficiente para elegir entre ellas.

## Licencia y uso

El dataset limpio y los cuadernos se comparten con fines de verificación y reproducibilidad. Si reutilizás este análisis, por favor citá tanto a TGEU como a Caribe Afirmativo como fuentes originales de los datos subyacentes, y a este repositorio como fuente del procesamiento y los modelos estadísticos aplicados.